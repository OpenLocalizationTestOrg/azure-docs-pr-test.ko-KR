---
title: "Microsoft Azure 및 Azure 모니터에서 경고 aaaOverview | Microsoft Docs"
description: "경고는 toomonitor Azure 리소스 메트릭, 이벤트 또는 로그 수 있도록 하 고 지정 된 조건이 충족 될 때 알림을 받으려면 합니다."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a6dea224-57bf-43d8-a292-06523037d70b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: robb
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d080080666fedc9eefda6b35cdea3714785d2223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-alerts-in-microsoft-azure"></a>Microsoft Azure의 경고란?
이 문서에서는 hello 이란 Microsoft Azure에서 경고의 다양 한 소스 hello 해당 경고의 이점 및 tooget을 사용 하 여 시작 하는 방법에 대 한 용도 설명 합니다. 특히 tooAzure 모니터를 적용 되지만 경고에 대 한 포인터 tooother 서비스를 제공 합니다. 경고는 hello 조건 최신 데이터를 모니터링 하는 hello와 일치 하는 경우 알림이 표시 되 고 데이터에 대해 tooconfigure 조건 수 있는 Azure에서 모니터링 하는 방법을 제공 합니다.

## <a name="taxonomy-of-azure-alerts"></a>Azure 경고의 분류
Azure 사용 하 여 hello 다음 toodescribe 경고와 해당 기능 조건:
* **경고** - 조건에 부합하면 활성화되는 기준의 정의(하나 이상의 규칙 또는 조건)
* **활성** -hello 경고에 의해 정의 된 조건을 만족 하는 경우 hello 상태입니다.
* **해결** -hello 후 이전에 충족 될 것에 경고에 의해 정의 된 조건을 충족 더 이상 때 hello 상태입니다.
* **알림** -hello 활성화 되기 경고 오프 기반으로 수행 하는 작업입니다.
* **작업** -(예를 들어 주소를 전자 메일로 전송 또는 tooa webhook URL을 게시) 알림을 전송 하는 특정 호출 tooa 수신기입니다. 알림은 보통 여러 작업을 트리거할 수 있습니다.

## <a name="alerts-in-different-azure-services"></a>다른 Azure 서비스에서의 경고
경고는 여러 Azure 모니터링 서비스전체 에서 제공됩니다. 방법 및 시기 toouse 이러한 서비스에 대 한 내용은 [이 문서를 참조 하십시오.](./monitoring-overview.md)합니다. Azure 전체에서 사용할 수 있는 hello 경고 유형에 대 한 분석을 같습니다.

| 부여 | 경고 유형 | 지원되는 서비스 | 설명 |
|---|---|---|---|
| Azure Monitor | [메트릭 경고](./insights-alerts-portal.md) | [Azure Monitor에서 지원되는 메트릭](./monitoring-supported-metrics.md) | 모든 플랫폼 수준 메트릭을 특정 조건을 충족 하는 경우 알림을 받게 (예를 들어 VM의 CPU (%) 보다 크면 hello에 대 한 90 지난 5 분)입니다. |
| Azure Monitor | [활동 로그 경고](./monitoring-activity-log-alerts.md) | Azure Resource Manager에서 사용 가능한 모든 리소스 유형 | 있는 경우 알림의 받을 hello에 새 이벤트 [Azure 활동 로그](./monitoring-overview-activity-logs.md) 변수나 특정 조건 ("VM 삭제" 작업 myProductionResourceGroup에서 발생 하는 경우에 예를 들어 "활성"으로 새 서비스 상태 이벤트를 hello 상태가 표시) 됩니다. |
| Application Insights | [메트릭 경고](../application-insights/app-insights-alerts.md) | 모든 응용 프로그램 계측 toosend 데이터 tooApplication Insights | 응용 프로그램 수준 메트릭이 특정 조건에 부합하면(예: 서버 응답 시간이 2초를 넘음) 알림을 받습니다. |
| Application Insights | [웹 테스트 경고](../application-insights/app-insights-monitor-web-app-availability.md) | 모든 웹 사이트 toosend 데이터 tooApplication Insights 계측 | 웹 사이트의 가용성이나 응답성이 기대 이하이면 알림을 받습니다. |
| Log Analytics | [Log Analytics 경고](../log-analytics/log-analytics-alerts.md) | 모든 서비스는 로그 분석에 toosend 데이터를 구성합니다. | 메트릭 및/또는 이벤트 데이터에 대한 Log Analytics 검색 쿼리가 특정 기준에 부합하면 알림을 받습니다. |

## <a name="alerts-on-azure-monitor-data"></a>Azure Monitor 데이터에 대한 경고
Azure Monitor에서는 메트릭 경고와 활동 로그 경고 등, 두 가지 유형의 데이터 경고를 제공합니다.

* **메트릭 경고** -지정 된 메트릭 hello 값 할당 하는 임계값을 초과할 때이 경고를 트리거합니다. hello 경고 hello 경고가 활성화 될 때"" (hello 임계값을 hello 경고 조건이 충족) 하면 때 처럼 "자동적으로 해결 되므로" (hello 임계값 다시 및 hello 조건이 더 이상 충족) 경우 알림을 생성 합니다. Azure Monitor에서 지원하는 사용 가능한 메트릭 목록은 [Azure Monitor에서 지원되는 메트릭 목록](monitoring-supported-metrics.md)을 참조하세요.
* **활동 로그 경고** - 사용자가 할당한 필터 기준에 부합하는 활동 로그 이벤트가 생성되면 트리거되는 스트리밍 로그 알림입니다. 이러한 경고는 하나만 상태가 "," 이후 활성화 hello 알림 엔진은 단순히 hello tooany 새 이벤트 필터 조건을 적용 합니다. 새 서비스 상태 사고가 발생 하는 경우 알림을 사용 하는 toobecome 수 또는 사용자나 응용 프로그램 구독에서 예를 들어 "가상 컴퓨터를 삭제" 작업을 수행할 때 이러한 경고 수 있습니다.

Azure 모니터를 통해 사용할 수 있는 진단 로그 데이터에 대 한 로그 분석 및 로그 분석 경고를 사용 하 여로 라우팅 hello 데이터를 권장 합니다. hello 다음 다이어그램에서는 요약 Azure 모니터 및에서는 개념적으로 해당 데이터를 경고할 수 있습니다 어떻게 데이터 소스에 합니다.

![경고를 설명합니다.](./media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="how-do-i-receive-a-notification-on-an-azure-monitor-alert"></a>Azure Monitor 경고에서 알림을 받는 방법
지금까지 다양한 서비스의 Azure 경고는 자체 기본 제공 알림 방법을 사용했습니다.  이제부터 Azure Monitor는 작업 그룹이라고 하는 재사용 가능한 알림 그룹화를 제공합니다. -전자 메일 주소를 개수에 관계 없이, (SMS)에 대 한 전화 번호 또는 webhook Url--알림에 대 한 수신자의 집합을 지정 하는 동작 그룹 및 hello 동작 그룹을 참조 하는 경고가 활성화 될 때마다 모든 수신자 해당 알림을 수신 합니다. 따라서 있습니다 tooreuse를 수신자 (예를 들어 on 통화 엔지니어 목록)의 그룹화 많은 경고 개체. 현재 활동 로그 경고만 작업 그룹ㅇ르 사용하지만 다른 몇 가지 Azure 경고 유형도 작업 그룹을 사용하기 위해 작업 중에 있습니다.

동작 그룹에 더하기 tooemail 주소와 SMS 번호 tooa webhook URL을 게시 하 여 알림을 지원 합니다. 이 때문에 다음 예시 항목을 사용하여 자동화 및 조치를 구현할 수 있습니다.
    - Azure Automation Runbook
    - Azure Function
    - Azure Logic App
    - 타사 서비스

메트릭 경고는 아직 작업 그룹을 사용하지 않습니다. 개별 메트릭 경고에서는 다음을 위해 알림을 구성할 수 있습니다.
* 알림 toohello 서비스 관리자, tooco 관리자 또는 tooadditional 전자 메일 주소 지정 하는 전자 메일을 보냅니다.
* 사용할 수 있는 webhook을 toolaunch 추가 자동화 작업을 호출 합니다.

## <a name="next-steps"></a>다음 단계
다음을 사용하여 경고 규칙에 대한 정보를 확인하고 구성할 수 있습니다.

* [메트릭](monitoring-overview-metrics.md)에 대해 자세히 알아보기
* [Azure Portal을 통해 메트릭 경고](insights-alerts-portal.md) 구성
* [메트릭 경고 PowerShell](insights-alerts-powershell.md) 구성
* [메트릭 경고 CLI(명령줄 인터페이스)](insights-alerts-command-line-interface.md) 구성
* [메트릭 경고 Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx) 구성
* [활동 로그](monitoring-overview-activity-logs.md)에 대해 자세히 알아보기
* [Azure Portal을 통해 활동 로그 경고](monitoring-activity-log-alerts.md) 구성
* [Resource Manager를 통해 활동 로그 경고](monitoring-create-activity-log-alerts-with-resource-manager-template.md) 구성
* 검토 hello [활동 로그 경고 webhook 스키마](monitoring-activity-log-alerts-webhook.md)
* [서비스 알림](monitoring-service-notifications.md)에 대해 자세히 알아보기
* [작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보기

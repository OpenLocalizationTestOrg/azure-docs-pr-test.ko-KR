---
title: "aaaMonitor Azure 모니터를 사용 하 여 API 관리 | Microsoft Docs"
description: "Azure 모니터를 사용 하 여 Azure API 관리 toomonitor을 서비스 하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a>Azure Monitor를 사용하여 API Management 모니터링
Azure Monitor는 모든 Azure 리소스 모니터링을 위한 단일 소스를 제공하는 Azure 서비스입니다. Azure 모니터를 사용 시각화, 쿼리, 경로, 보관 하 고 수 hello 메트릭 및 API 관리와 같은 Azure 리소스에서 오는 로그 작업을 수행 합니다. 

비디오 표시 방법을 따르는 hello toomonitor Azure 모니터를 사용 하 여 API 관리 합니다. Azure Monitor에 대한 자세한 내용은 [Azure Monitor 시작]을 참조하세요. 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a>메트릭
API 관리에는 현재 5 개의 메트릭을 내보내는 이며 tooadd hello 향후에 더 많은 계획 합니다. 이러한 메트릭을 내보내지는 1 분 마다 근처 hello 상태 및 Api의 상태에 대 한 실시간 가시성을 제공 합니다. 다음은 hello 메트릭에 대 한 요약입니다.
* 게이트웨이 요청 합계: hello 기간에는 요청을 API hello 수입니다. 
* 304, 등 307 301 (예: 200) 보다 작은 대상 성공 HTTP 응답 코드를 받은 API 요청의 성공 게이트웨이 요청: hello 수입니다. 
* 실패 한 요청 수 게이트웨이: hello API 요청 수를 잘못 된 HTTP 응답 코드 400 및 500 보다 큰 모든 항목을 포함 하 여 받은입니다.
* 받은 HTTP 응답 코드 401, 403, 및 429를 포함 하 여 API 요청 인증 되지 않은 게이트웨이 요청 수: hello 수입니다. 
* API 요청 받은 HTTP 응답 코드의 앞에 범주 (예를 들어 418) hello tooany에 속하지 않는 다른 게이트웨이 요청: hello 수입니다.

API Management 서비스에서 메트릭에 액세스하거나 Azure Monitor에서 모든 Azure 리소스의 메트릭에 액세스할 수 있습니다. API 관리 서비스에서 tooview 메트릭:
1. Azure 포털 hello를 엽니다.
2. Tooyour API 관리 서비스를 이동 합니다.
3. **메트릭**을 클릭합니다.

![메트릭 블레이드][metrics-blade]

방법에 대 한 자세한 정보에 대 한 메트릭, toouse 참조 [메트릭 개요]합니다.

## <a name="activity-logs"></a>활동 로그
활동 로그 API 관리 서비스에서 수행 된 hello 작업에 대 한 정보를 제공 합니다. 이전에는 이러한 로그를 "감사 로그" 또는 "작업 로그"라고도 했습니다. 작업 로그를 사용 하 여 hello 확인할 수 있습니다 "부분, who, 시기 및" 모든 쓰기 작업 (PUT, POST, DELETE) API 관리 서비스에 대해 수행에 대 한 합니다. 

> [!NOTE]
> 읽기 (GET) 작업이 나에서 수행 된 작업 활동 로그를 포함 하지 않는 hello 클래식 게시자 포털 또는 관리 Api를 원래 hello를 사용 하 여 합니다.

API Management 서비스에서 활동 로그에 액세스하거나 Azure Monitor에서 모든 Azure 리소스의 로그에 액세스할 수 있습니다. API 관리 서비스에서 tooview 활동 기록합니다.
1. Azure 포털 hello를 엽니다.
2. Tooyour API 관리 서비스를 이동 합니다.
3. **활동 로그**를 클릭합니다.

![활동 로그 블레이드][activity-logs-blade]

방법에 대 한 자세한 내용은 toouse 메트릭 참조 [활동 로그 개요]합니다.

## <a name="alerts"></a>경고
메트릭 및 활동 로그를 기반으로 하는 tooreceive 경고를 구성할 수 있습니다. Azure 모니터 표시할 때을 다음 경고 toodo hello tooconfigure가 있습니다.

* 전자 메일 알림 보내기
* 웹후크 호출
* Azure 논리 앱 호출

API Management 서비스 또는 Azure Monitor에서 경고 규칙을 구성할 수 있습니다. tooconfigure API 관리에서 해당: 
1. Azure 포털 hello를 엽니다.
2. Tooyour API 관리 서비스를 이동 합니다.
3. **경고 규칙**을 클릭합니다.

![경고 규칙 블레이드][alert-rules-blade]

경고 사용에 대한 자세한 내용은 [경고 개요]를 참조하세요.

## <a name="diagnostic-logs"></a>진단 로그
진단 로그는 감사 뿐만 아니라 문제 해결에 중요한 작업 및 오류에 대한 풍부한 정보를 제공합니다. 진단 로그는 활동 로그와 다릅니다. 작업 로그는 Azure 리소스에서 수행 된 hello 작업에 대 한 정보를 제공 합니다. 진단 로그는 리소스 자체에서 수행하는 작업에 대한 정보를 제공합니다.

API 관리에는 현재 진단을 제공 hello 구조를 다음 있는 각 항목에 개별 API에 대 한 로그 (매시간 일괄 처리) 요청:

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

API Management 서비스에서 진단 로그에 액세스하거나 Azure Monitor에서 모든 Azure 리소스의 로그에 액세스할 수 있습니다. API 관리 서비스에서 진단 로그 tooview:
1. Azure 포털 hello를 엽니다.
2. Tooyour API 관리 서비스를 이동 합니다.
3. **진단 로그**를 클릭합니다.

![진단 로그 블레이드][diagnostic-logs-blade]

방법에 대 한 자세한 정보에 대 한 메트릭, toouse 참조 [진단 로그의 개요]합니다.

## <a name="next-step"></a>다음 단계

* [Azure Monitor 시작]
* [메트릭 개요]
* [활동 로그 개요]
* [진단 로그의 개요]
* [경고 개요]

[Azure Monitor 시작]: ../monitoring-and-diagnostics/monitoring-get-started.md
[메트릭 개요]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[활동 로그 개요]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[진단 로그의 개요]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[경고 개요]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png

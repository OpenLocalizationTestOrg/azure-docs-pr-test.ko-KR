---
title: "Azure Web Apps 분석 데이터 보기 | Microsoft Docs"
description: "Azure Web Apps 분석 솔루션을 사용하여 모든 Azure Web Apps 리소스의 다양한 메트릭을 수집함으로써 Azure Web Apps에 대한 자세한 정보를 얻을 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 20ff337f-b1a3-4696-9b5a-d39727a94220
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: banders
ms.openlocfilehash: d910339cc35e09705e543706b40dfe8e0ea9dd42
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2017
---
# <a name="view-analytic-data-for-metrics-across-all-your-azure-web-app-resources"></a>모든 Azure Web Apps 리소스의 메트릭에 대한 분석 데이터 보기

![Web Apps 기호](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)  
Azure Web Apps 분석(미리 보기) 솔루션은 모든 Azure Web Apps 리소스의 다양한 메트릭을 수집함으로써 [Azure Web Apps](../app-service/app-service-web-overview.md)에 대한 자세한 정보를 제공합니다. 이 솔루션을 사용하여 웹앱 리소스 메트릭 데이터를 분석하고 검색할 수 있습니다.

이 솔루션을 사용하면 다음을 확인할 수 있습니다.

- 가장 높은 응답 시간을 보인 상위 Web Apps
- 성공 및 실패한 요청을 포함하는 Web Apps의 요청 수
- 들어오고 나가는 트래픽이 가장 높은 상위 Web Apps
- 높은 CPU 및 메모리 사용률을 보이는 상위 서비스 계획
- Azure Web Apps 활동 로그 작업

## <a name="connected-sources"></a>연결된 소스

대부분의 다른 Log Analytics 솔루션과는 달리, 에이전트에서 Azure Web Apps에 대한 데이터를 수집하지 않습니다. 솔루션에서 사용하는 모든 데이터는 Azure에서 직접 옵니다.

| 연결된 소스 | 지원됨 | 설명 |
| --- | --- | --- |
| [Windows 에이전트](log-analytics-windows-agent.md) | 아니요 | 솔루션이 Windows 에이전트에서 정보를 수집하지 않습니다. |
| [Linux 에이전트](log-analytics-linux-agents.md) | 아니요 | 솔루션이 Linux 에이전트에서 정보를 수집하지 않습니다. |
| [SCOM 관리 그룹](log-analytics-om-agents.md) | 아니요 | 솔루션이 연결된 SCOM 관리 그룹의 에이전트에서 정보를 수집하지 않습니다. |
| [Azure 저장소 계정](log-analytics-azure-storage.md) | 아니요 | 솔루션이 Azure Storage에서 정보를 수집하지 않습니다. |

## <a name="prerequisites"></a>필수 조건

- Azure Web App 리소스 메트릭 정보에 액세스하려면 Azure 구독이 있어야 합니다.

## <a name="configuration"></a>구성

다음 단계를 수행하여 작업 영역에 대해 Azure Web Apps 분석 솔루션을 구성합니다.

1. [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview)에서 또는 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에서 설명한 프로세스를 사용하여 Azure Web Apps 분석 솔루션을 사용하도록 설정합니다.
2. [PowerShell을 사용하여 OMS에 대한 Azure 리소스 메트릭 로깅을 사용하도록 설정](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell)합니다.

Azure Web Apps 분석 솔루션은 Azure에서 다음과 같은 두 가지 메트릭 집합을 수집합니다.

- Azure Web Apps 메트릭
  - 평균 메모리 작업 집합
  - 평균 응답 시간
  - 받은 바이트/보낸 바이트
  - CPU 시간
  - 요청
  - 메모리 작업 집합
  - Httpxxx
- App Service 계획 메트릭
  - 받은 바이트/보낸 바이트
  - CPU 비율
  - 디스크 큐 길이
  - Http 큐 길이
  - 메모리 비율

전용 서비스 계획을 사용하는 경우 App Service 계획 메트릭이 수집됩니다. 무료 또는 공유 App Service 계획에는 적용되지 않습니다.

OMS 포털을 사용하여 솔루션을 추가하면 다음 타일이 표시됩니다. [PowerShell을 사용하여 OMS에 대한 Azure 리소스 메트릭 로깅을 사용하도록 설정](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell)해야 합니다.

![평가 알림 수행](./media/log-analytics-azure-web-apps-analytics/performing-assessment.png)

이 솔루션을 구성한 후 15분 내에 작업 영역으로 데이터가 흐르기 시작해야 합니다.

## <a name="using-the-solution"></a>솔루션 사용

Azure Web Apps 분석 솔루션을 작업 영역에 추가하면 개요 대시보드에 **Azure Web Apps 분석** 타일이 추가됩니다. 이 타일에는 솔루션에서 액세스할 수 있는 Azure 구독의 Azure Web Apps 수가 표시됩니다.

![Azure Web Apps 분석 타일](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-tile.png)

### <a name="view-azure-web-apps-analytics-information"></a>Azure Web Apps 분석 정보 보기

**Azure Web Apps 분석** 타일을 클릭하여 **Azure Web Apps 분석** 대시보드를 엽니다. 대시보드에는 다음 테이블의 블레이드가 포함되어 있습니다. 각 블레이드에는 지정된 범위 및 시간 범위에 대한 해당 블레이드의 기준과 일치하는 항목이 최대 10개까지 나열됩니다. 블레이드 맨 아래에서 **모두 보기**를 클릭하거나 블레이드 헤더를 클릭하여 모든 레코드를 반환하는 로그 검색을 실행할 수 있습니다.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| 열 | 설명 |
| --- | --- |
| Azure Webapps |   |
| Web Apps 요청 추세 | 선택한 날짜 범위에 대한 Web Apps 요청 추세의 꺾은선형 차트를 표시하고 상위 10개의 웹 요청 목록을 표시합니다. 꺾은선형 차트를 클릭하여 <code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code>에 대한 로그 검색을 실행합니다. <br>웹 요청 항목을 클릭하면 요청된 웹 요청 메트릭 추세에 대한 로그 검색이 실행됩니다. |
| Web Apps 응답 시간 | 선택한 날짜 범위에 대한 Web Apps 응답 시간의 꺾은선형 차트를 보여 줍니다. 상위 10개 Web Apps 응답 시간도 표시됩니다. 차트를 클릭하면 <code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code>에 대한 로그 검색이 실행됩니다.<br> 웹앱을 클릭하여 웹앱에 대한 응답 시간을 반환하는 로그 검색을 실행합니다. |
| Web Apps 트래픽 | Web Apps 트래픽(MB 단위)에 대한 꺾은선형 차트를 표시하고 상위 Web Apps 트래픽을 표시합니다. 차트를 클릭하면 <code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code>에 대한 로그 검색이 실행됩니다.<br> 마지막 1분 동안 트래픽이 발생한 모든 Web Apps가 표시됩니다. 웹앱을 클릭하면 웹앱에 대해 받은 바이트 및 보내 바이트를 표시하는 로그 검색이 실행됩니다. |
| Azure App Service 계획 |   |
| CPU 사용률이 &gt; 80%인 App Service 계획 | CPU 사용률이 80%를 초과하는 App Service 계획의 총 수를 표시하고 CPU 사용률별 상위 10개의 App Service 계획을 나열합니다. 합계 영역을 클릭하여 <code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code>에 대한 로그 검색을 실행합니다.<br> App Service 계획 및 평균 CPU 사용률 목록이 표시됩니다. App Service 계획을 클릭하면 평균 CPU 사용률을 보여 주는 로그 검색이 실행됩니다. |
| 메모리 사용률이 &gt; 80%인 App Service 계획 | 메모리 사용률이 80%를 초과하는 App Service 계획의 총 수를 표시하고 메모리 사용률별 상위 10개의 App Service 계획을 나열합니다. 합계 영역을 클릭하여 <code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code>에 대한 로그 검색을 실행합니다.<br> App Service 계획 및 평균 메모리 사용률 목록이 표시됩니다. App Service 계획을 클릭하면 평균 메모리 사용률을 보여 주는 로그 검색이 실행됩니다. |
| Azure Web Apps 활동 로그 |   |
| Azure Web Apps 활동 감사 | [활동 로그](log-analytics-activity.md)가 있는 Web Apps의 총 수를 표시하고 상위 10개의 활동 로그 작업을 나열합니다. 합계 영역을 클릭하여 <code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code>에 대한 로그 검색을 실행합니다.<br> 활동 로그 작업의 목록이 표시됩니다. 활동 로그 작업을 클릭하면 작업에 대한 레코드를 나열하는 로그 검색이 실행됩니다. |



### <a name="azure-web-apps"></a>Azure Web Apps

대시보드에서 드릴다운하여 Web Apps 메트릭에 대한 자세한 정보를 볼 수 있습니다. 첫 번째 블레이드 집합에는 시간에 따른 Web Apps 요청의 추세, 오류 수(예: HTTP404), 트래픽 및 평균 응답 시간이 표시됩니다. 또한 다른 Web Apps에 대한 해당 메트릭 분석 결과도 표시됩니다.

![Azure Webapps 블레이드](./media/log-analytics-azure-web-apps-analytics/web-apps-dash01.png)

이러한 데이터를 표시하는 주요 이유는 응답 시간이 높은 웹앱을 식별하고 근본 원인의 조사하여 알아낼 수 있도록 하기 위한 것입니다. 문제가 있는 App Services를 보다 쉽게 식별하는 데 도움을 주기 위해 임계값 제한도 적용됩니다.

- 빨간색으로 표시되는 Web Apps는 응답 시간이 1초보다 깁니다.
- 주황색으로 표시되는 Web Apps는 응답 시간이 0.7초보다 길고 1초보다 짧습니다.
- 녹색으로 표시되는 Web Apps는 응답 시간이 0.7초보다 짧습니다.

다음 로그 검색 예제 이미지에서는 *anugup3* 웹앱이 다른 웹앱보다 응답 시간이 훨씬 더 높다는 사실을 확인할 수 있습니다.

![로그 검색 예제](./media/log-analytics-azure-web-apps-analytics/web-app-search-example.png)

### <a name="app-service-plans"></a>App Service 계획

전용 서비스 계획을 사용하는 경우 App Service 계획에 대한 메트릭을 수집할 수도 있습니다. 이 보기에서는 CPU 또는 메모리 사용률이 높은(&gt; 80%) App Service 계획이 표시됩니다. 메모리 또는 CPU 사용률이 높은 상위 App Services도 표시됩니다. 마찬가지로 문제가 있는 App Services를 보다 쉽게 식별하는 데 도움을 주기 위해 임계값 제한이 적용됩니다.

- 빨간색으로 표시되는 App Service 계획은 CPU/메모리 사용률이 80%보다 높습니다.
- 주황색으로 표시되는 App Service 계획은 CPU/메모리 사용률이 60%보다 높고 80%보다 낮습니다.
- 녹색으로 표시되는 App Service 계획은 CPU/메모리 사용률이 60%보다 낮습니다.

![Azure App Service 계획 블레이드](./media/log-analytics-azure-web-apps-analytics/web-apps-dash02.png)

## <a name="azure-web-apps-log-searches"></a>Azure Web Apps 로그 검색

**인기 있는 Azure Web Apps 검색 쿼리 목록**에는 Web Apps 리소스에 대해 수행된 작업에 대한 자세한 정보를 제공하는 Web Apps에 대한 모든 관련 활동 로그가 표시됩니다. 또한 모든 관련 작업 및 발생한 횟수도 표시됩니다.

로그 검색 쿼리에서 시작하면 경고를 쉽게 만들 수 있습니다. 예를 들어 메트릭의 평균 응답 시간이 1초보다 클 때 경고를 만들 수도 있습니다.

## <a name="next-steps"></a>다음 단계

- 특정 메트릭에 대한 [경고](log-analytics-alerts-creating.md)를 만듭니다.
- [로그 검색](log-analytics-log-searches.md)을 사용하여 활동 로그의 자세한 정보를 봅니다.

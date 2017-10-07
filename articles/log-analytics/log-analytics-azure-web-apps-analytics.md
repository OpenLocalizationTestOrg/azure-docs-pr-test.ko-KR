---
title: "Azure 웹 앱 분석 데이터 aaaView | Microsoft Docs"
description: "모든 Azure 웹 앱 리소스 간에 다른 메트릭을 수집 하 여 Azure 웹 앱에 대 한 hello Azure 웹 앱 분석 솔루션 toogain insights를 사용할 수 있습니다."
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
ms.openlocfilehash: 7e9725f95c9faf01da89184975ad5444dd19ff95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="view-analytic-data-for-metrics-across-all-your-azure-web-app-resources"></a>모든 Azure Web Apps 리소스의 메트릭에 대한 분석 데이터 보기

![웹앱 기호](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)  
hello Azure 웹 앱 분석 (미리 보기) 솔루션에 대 한 정보를 제공 하면 [Azure 웹 앱](../app-service-web/app-service-web-overview.md) 모든 Azure 웹 앱 리소스 간에 다른 메트릭을 수집 하 여 합니다. Hello 솔루션을 사용 하 여 분석 하 고 웹 응용 프로그램 리소스에 대 한 메트릭 데이터를 검색할 수 있습니다.

볼 수 hello 솔루션을 사용 하 여:

- Hello 최고 응답 시간을 사용 하 여 상위 웹 앱
- 성공 및 실패한 요청을 포함하는 웹앱의 요청 수
- 들어오고 나가는 트래픽이 가장 높은 상위 웹앱
- 높은 CPU 및 메모리 사용률을 보이는 상위 서비스 계획
- Azure Web Apps 활동 로그 작업

## <a name="connected-sources"></a>연결된 소스

대부분의 다른 Log Analytics 솔루션과는 달리, 에이전트에서 Azure Web Apps에 대한 데이터를 수집하지 않습니다. Hello 솔루션에서 사용 하는 모든 데이터는 Azure에서 직접 제공 됩니다.

| 연결된 소스 | 지원됨 | 설명 |
| --- | --- | --- |
| [Windows 에이전트](log-analytics-windows-agents.md) | 아니요 | hello 솔루션 Windows 에이전트에서 정보를 수집 하지 않습니다. |
| [Linux 에이전트](log-analytics-linux-agents.md) | 아니요 | hello 솔루션 Linux 에이전트에서 정보를 수집 하지 않습니다. |
| [SCOM 관리 그룹](log-analytics-om-agents.md) | 아니요 | hello 솔루션 연결된 SCOM 관리 그룹의 에이전트에서 정보를 수집 하지 않습니다. |
| [Azure 저장소 계정](log-analytics-azure-storage.md) | 아니요 | hello 솔루션은 Azure 저장소에서 컬렉션 정보 없습니다. |

## <a name="prerequisites"></a>필수 조건

- Azure 웹 앱 리소스에 대 한 메트릭 정보 tooaccess Azure 구독이 있어야 합니다.

## <a name="configuration"></a>구성

Hello 단계 tooconfigure hello Azure 웹 앱 분석 솔루션의 작업 영역에 대 한 다음을 수행 합니다.

1. Hello Azure 웹 앱 분석 솔루션에서 사용 하도록 설정 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.
2. [PowerShell을 사용 하 여 Azure 리소스 메트릭 로깅 tooOMS 사용](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell)합니다.

hello Azure 웹 앱 분석 솔루션은 Azure에서 메트릭 집합이 두 개를 수집합니다.

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

전용 서비스 계획을 사용하는 경우 App Service 계획 메트릭이 수집됩니다. 이 toofree 적용 되지 않습니다 또는 앱 서비스 계획을 공유 합니다.

Hello OMS 포털을 사용 하 여 hello 솔루션을 추가한 경우 hello 다음 타일을 볼 수 있습니다. 너무 필요한[PowerShell을 사용 하 여 Azure 리소스 메트릭 로깅 tooOMS 사용](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell)합니다.

![평가 알림 수행](./media/log-analytics-azure-web-apps-analytics/performing-assessment.png)

데이터 전송이 시작 해야 hello 솔루션을 구성한 후 15 분 이내 tooyour 작업 영역입니다.

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여

Hello Azure 웹 앱 분석 솔루션 tooyour 작업 영역에 추가 하면 hello **Azure 웹 앱 분석** 타일 tooyour 개요 대시보드에 추가 됩니다. 이 타일 hello 수의 hello 솔루션은 Azure 구독 액세스 tooin는 Azure 웹 앱의 수를 표시 합니다.

![Azure Web Apps 분석 타일](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-tile.png)

### <a name="view-azure-web-apps-analytics-information"></a>Azure Web Apps 분석 정보 보기

Hello 클릭 **Azure 웹 앱 분석** 타일 tooopen hello **Azure 웹 앱 분석** 대시보드 합니다. hello 대시보드는 다음 표에 hello에 hello 블레이드를 포함 합니다. 각 블레이드 hello에 대 한 조건을 블레이드 범위 및 시간 범위를 지정 했는지 일치 tooten 항목을 나열 합니다. 클릭 하 여 모든 레코드를 반환 하는 로그 검색을 실행할 수 있습니다 **스크롤하게** hello 블레이드의 또는 hello 블레이드 헤더를 클릭 하 여 hello 맨 아래에 있습니다.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| 열 | 설명 |
| --- | --- |
| Azure Webapps |   |
| 웹앱 요청 추세 | Hello 상위 10 개의 웹 요청 목록이 표시 및 선택한 hello 날짜 범위에 대 한 웹 응용 프로그램 요청 추세 hello의 꺾은선형 차트를 보여 줍니다. 꺾은선형 차트 toorun hello에 대 한 로그 검색을 클릭<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code> <br>웹 요청 항목 toorun 요청 hello 웹 요청 메트릭 추세에 대 한 로그 검색을 클릭 합니다. |
| 웹앱 응답 시간 | 선택한 hello 날짜 범위에 대 한 hello 웹 응용 프로그램 응답 시간에 꺾은선형 차트를 보여 줍니다. 목록 hello 목록 보여 주는 또한 상위 10 개의 웹 응용 프로그램 응답 시간이 됩니다. 에 대 한 로그 검색 hello 차트 toorun를 클릭 합니다.<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code><br> 웹 앱 toorun hello 웹 앱에 대 한 응답 시간을 반환 하는 로그 검색을 클릭 합니다. |
| 웹앱 트래픽 | Mb에서 웹 앱 트래픽의 경우 꺾은선형 차트를 표시 하 고 hello 상위 웹 앱 트래픽을 나열 합니다. 에 대 한 로그 검색 hello 차트 toorun를 클릭 합니다.<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code><br> 지난 1 분간 hello에 대 한 트래픽이 모든 웹 응용 프로그램을 표시합니다. 바이트를 보여 주는 로그 검색을 보내고 받은 hello 웹 앱에 대 한 웹 앱 toorun를 클릭 합니다. |
| Azure App Service 계획 |   |
| CPU 사용률이 &gt; 80%인 App Service 계획 | Hello CPU 사용률이 80%와 목록 hello 상위 10 개의 앱 서비스 계획에서 CPU 사용률 보다 큰 값이 있는 앱 서비스 계획의 총 수를 보여 줍니다. 에 대 한 로그 검색 hello 전체 영역의 toorun를 클릭 합니다.<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code><br> App Service 계획 및 평균 CPU 사용률 목록이 표시됩니다. 앱 서비스 계획 toorun의 평균 CPU 사용률을 보여 주는 로그 검색을 클릭 합니다. |
| 메모리 사용률이 &gt; 80%인 App Service 계획 | Hello 메모리 사용률이 80%와 목록 hello 상위 10 개의 앱 서비스 계획의 메모리 사용률 하 여 보다 큰 값이 있는 앱 서비스 계획의 총 수를 보여 줍니다. 에 대 한 로그 검색 hello 전체 영역의 toorun를 클릭 합니다.<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code><br> App Service 계획 및 평균 메모리 사용률 목록이 표시됩니다. 앱 서비스 계획 toorun의 평균 메모리 사용률을 보여 주는 로그 검색을 클릭 합니다. |
| Azure Web Apps 활동 로그 |   |
| Azure Web Apps 활동 감사 | 표시 된 웹 응용 프로그램의 총 수 hello [활동 로그](log-analytics-activity.md) 목록 hello 상위 10 개의 활동 로그 작업 및 합니다. 에 대 한 로그 검색 hello 전체 영역의 toorun를 클릭 합니다.<code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code><br> 활동 로그 작업 hello 목록을 보여 줍니다. 활동 로그 작업 toorun hello 작업에 대 한 hello 레코드를 나열 하는 로그 검색을 클릭 합니다. |



### <a name="azure-web-apps"></a>Azure 웹앱

Hello 대시보드에 tooget 다운 웹 응용 프로그램 메트릭 볼 수 있게를 드릴 수 있습니다. 이 첫 번째 집합 블레이드 중 시간이 지남에 따라 hello 웹 응용 프로그램 요청, 오류 (예를 들어 HTTP404), 트래픽 및 평균 응답 시간 수의 hello 추세를 표시 합니다. 또한 다른 웹앱에 대한 해당 메트릭 분석 결과도 표시됩니다.

![Azure Webapps 블레이드](./media/log-analytics-azure-web-apps-analytics/web-apps-dash01.png)

높은 응답 시간으로 웹 응용 프로그램을 식별 하 고 toofind hello 근본 원인을 조사할 수 있도록 데이터를 표시 하는 데 사용 되는 주요 이유입니다. 임계값 제한을 적용 된 toohelp 문제 형식과 hello에 보다 쉽게 식별할 수 이기도 합니다.

- 빨간색으로 표시되는 웹앱은 응답 시간이 1초보다 깁니다.
- 주황색으로 표시되는 웹앱은 응답 시간이 0.7초보다 길고 1초보다 짧습니다.
- 녹색으로 표시되는 웹앱은 응답 시간이 0.7초보다 짧습니다.

다음 예에서는 이미지를 검색 하는 로그 hello, 해당 hello를 볼 수 있습니다 *anugup3* 웹 앱에 다른 웹 앱 hello 보다 훨씬 더 높은 응답 시간입니다.

![로그 검색 예제](./media/log-analytics-azure-web-apps-analytics/web-app-search-example.png)

### <a name="app-service-plans"></a>앱 서비스 계획

전용 서비스 계획을 사용하는 경우 App Service 계획에 대한 메트릭을 수집할 수도 있습니다. 이 보기에서는 CPU 또는 메모리 사용률이 높은(&gt; 80%) App Service 계획이 표시됩니다. 또한 표시 hello 메모리 또는 CPU 사용률이 높은 상위 응용 프로그램 서비스입니다. 마찬가지로, 임계값 제한이 적용 된 toohelp 문제 형식과 hello에 보다 쉽게 식별할 수 있습니다.

- 빨간색으로 표시되는 App Service 계획은 CPU/메모리 사용률이 80%보다 높습니다.
- 주황색으로 표시되는 App Service 계획은 CPU/메모리 사용률이 60%보다 높고 80%보다 낮습니다.
- 녹색으로 표시되는 App Service 계획은 CPU/메모리 사용률이 60%보다 낮습니다.

![Azure App Service 계획 블레이드](./media/log-analytics-azure-web-apps-analytics/web-apps-dash02.png)

## <a name="azure-web-apps-log-searches"></a>Azure Web Apps 로그 검색

hello **목록의 인기 있는 Azure 웹 앱 검색 쿼리** 모든 hello를 보면 관련 웹 응용 프로그램 리소스에서 수행 된 hello 작업에 대 한 정보를 제공 하는 웹 앱에 대 한 활동 로그 합니다. 또한 나열 모든 hello 관련 작업 및 hello 여러 번 발생 했을 때입니다.

Hello 로그 검색 쿼리 중 하나를 사용 하 여 시작 지점으로, 경고를 쉽게 만들 수 있습니다. 예를 들어 좋습니다 toocreate 경고 메트릭을 평균 응답 시간 1 초 보다 큰 경우.

## <a name="next-steps"></a>다음 단계

- 특정 메트릭에 대한 [경고](log-analytics-alerts-creating.md)를 만듭니다.
- 사용 하 여 [로그 검색](log-analytics-log-searches.md) tooview 활동 로그에서 정보를 자세히 설명 합니다.

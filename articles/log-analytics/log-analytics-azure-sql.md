---
title: "로그 분석에서 SQL 분석 솔루션 aaaAzure | Microsoft Docs"
description: "Azure SQL 분석 솔루션 hello Azure SQL 데이터베이스를 관리할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>Log Analytics에 Azure SQL Analytics(미리 보기)를 사용하여 Azure SQL Database 모니터링

![Azure SQL 분석 기호](./media/log-analytics-azure-sql/azure-sql-symbol.png)

Azure 로그 분석에서 Azure SQL 분석 솔루션 hello 수집 하 고 중요 한 SQL Azure 성능 메트릭 시각화 합니다. Hello 메트릭을 수집 하는 hello 솔루션과 사용 하 여 사용자 지정 모니터링 규칙 및 경고를 만들 수 있습니다. 그리고 여러 Azure 구독 및 탄력적 풀 간에 Azure SQL Database 및 탄력적 풀 메트릭을 모니터링하고 이를 시각화할 수 있습니다. hello 솔루션의 응용 프로그램 스택의 각 계층에서 tooidentify 문제 수 있습니다.  사용 하 여 [Azure 진단 메트릭은](log-analytics-azure-storage.md) 로그 분석 함께 단일 로그 분석 작업 영역에서 모든 Azure SQL 데이터베이스 및 탄력적인 풀에 대 한 toopresent 데이터를 봅니다.

현재,이 미리 보기 솔루션 too150, 000 Azure SQL 데이터베이스 및 작업 영역당 5, 000 SQL 탄력적 풀을 지원합니다.

로그 분석에 사용할 수 있는 다른 처럼 Azure SQL 분석 솔루션 hello를 사용 하면 모니터링 하 고 Azure 리소스의 hello 상태에 대 한 알림을 받을-이 경우, Azure SQL 데이터베이스입니다. Microsoft Azure SQL 데이터베이스는 Azure 클라우드 hello에서 실행 되는 친숙 한 SQL 서버 유형의 기능 tooapplications 제공 하는 확장 가능한 관계형 데이터베이스 서비스입니다. 로그 분석 하면 toocollect, 상관 관계를 분석 하 고 데이터 및 구조화 되지 않은 데이터를 시각화 합니다.

## <a name="connected-sources"></a>연결된 소스

Azure SQL 분석 솔루션 hello 에이전트 tooconnect toohello 로그 분석 서비스를 사용 하지 않습니다.

다음 표에서 hello이이 솔루션에서 지원 되는 연결 된 hello 원본에 설명 합니다.

| 연결된 소스 | 지원 | 설명 |
| --- | --- | --- |
| [Windows 에이전트](log-analytics-windows-agents.md) | 아니요 | Windows 에이전트를 직접 hello 솔루션에서 사용 되지 않습니다. |
| [Linux 에이전트](log-analytics-linux-agents.md) | 아니요 | Linux 에이전트를 직접 hello 솔루션에서 사용 되지 않습니다. |
| [SCOM 관리 그룹](log-analytics-om-agents.md) | 아니요 | Hello SCOM 에이전트 tooLog 분석의에서 직접 연결 hello 솔루션에서 사용 되지 않습니다. |
| [Azure 저장소 계정](log-analytics-azure-storage.md) | 아니요 | 로그 분석 저장소 계정에서 hello 데이터를 읽지 않습니다. |
| [Azure 진단](log-analytics-azure-storage.md) | 예 | Azure 메트릭 데이터는 Azure에서 직접 tooLog 분석을 전송 됩니다. |

## <a name="prerequisites"></a>필수 조건

- Azure 구독. 없는 경우 [무료](https://azure.microsoft.com/free/) 구독을 하나 만들 수 있습니다.
- Log Analytics 작업 영역. 기존 항목을 사용하거나 이 솔루션 사용을 시작하기 전에 [새로 만들 수 있습니다.](log-analytics-get-started.md)
- Azure SQL 데이터베이스 및 탄력적인 풀에 대 한 Azure 진단을 사용 하도록 설정 하 고 [toosend 구성 자신의 데이터 tooLog 분석](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)합니다.

## <a name="configuration"></a>구성

Hello 단계 tooadd hello Azure SQL 분석 솔루션 tooyour 작업 영역을 다음을 수행 합니다.

1. Hello Azure SQL 분석 솔루션 tooyour 작업 영역에서 추가 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.
2. Hello Azure 포털에서에서 클릭 **새로** (hello + 기호) hello 목록에서 리소스를 선택 **모니터링 + 관리**합니다.  
    ![모니터링 + 관리](./media/log-analytics-azure-sql/monitoring-management.png)
3. Hello에 **모니터링 + 관리** 목록에서를 클릭 **스크롤하게**합니다.
4. Hello에 **권장** 목록에서 클릭 **자세한** , 했는데 이후에 hello 새 목록에 **Azure SQL 분석 (미리 보기)** 다음 선택 합니다.  
    ![Azure SQL Analytics 솔루션](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. Hello에 **Azure SQL 분석 (미리 보기)** 블레이드에서 클릭 **만들기**합니다.  
    ![만들기](./media/log-analytics-azure-sql/portal-create.png)
6. Hello에 **새 솔루션 만들기** 블레이드, 선택 hello 작업 영역 tooadd hello 솔루션 tooand 원하는 다음 클릭 있습니다 **만들기**합니다.  
    ![tooworkspace 추가](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="tooconfigure-multiple-azure-subscriptions"></a>tooconfigure 여러 Azure 구독

toosupport 여러 구독을 사용 하 여 hello PowerShell 스크립트를 [PowerShell을 사용 하 여 사용 하도록 설정 하는 Azure 리소스 메트릭 로깅](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)합니다. 다른 Azure 구독에 Azure 구독 하나 tooa 작업 영역에 리소스에서 hello 스크립트 toosend 진단 데이터를 실행할 때 매개 변수로 hello 작업 공간 리소스 ID를 제공 합니다.

**예제**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여

Hello 솔루션 tooyour 작업 영역에 추가 하면 Azure SQL 분석 타일 hello tooyour 작업 영역에 추가 됩니다 및 개요에 나타납니다. hello 타일에는 Azure SQL 데이터베이스 및 hello 솔루션에 연결 된 Azure SQL 탄력적 풀의 hello 수가 표시 됩니다.

![Azure SQL Analytics 타일](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>Azure SQL 분석 데이터 보기

Hello 클릭 **Azure SQL 분석** tooopen hello Azure SQL 분석 대시보드 타일입니다. hello 대시보드에 아래에 정의 된 hello 블레이드 포함 됩니다. 각 블레이드 too15 리소스 (구독, 서버, 탄력적 풀 및 데이터베이스)를 나열합니다. 해당 특정 리소스에 대 한 hello 리소스 tooopen hello 대시보드 중 하나를 클릭 합니다. 탄력적 풀 또는 데이터베이스에는 선택한 리소스에 대 한 메트릭 사용 하 여 hello 차트를 포함 합니다. 차트 tooopen hello 로그 검색 대화 상자를 클릭 합니다.

| 블레이드 | 설명 |
|---|---|
| 구독 | 연결된 서버, 풀 및 데이터베이스 수가 있는 구독 목록입니다. |
| 서버 | 연결된 풀 및 데이터베이스 수가 있는 서버 목록입니다. |
| 탄력적 풀 | 목록 최대 GB 인데 관찰 된 hello에 대 한 eDTU와 연결 된 탄력적 풀의 기간입니다. |
|데이터베이스 | Hello 관찰 된 최대 GB 인데 DTU와 연결 된 데이터베이스 목록을 기간입니다.|


### <a name="analyze-data-and-create-alerts"></a>데이터 분석 및 경고 만들기

Azure SQL 데이터베이스 리소스에서 들어오는 hello 데이터와 경고를 쉽게 만들 수 있습니다. 다음은 경고 생성에 사용할 수 있는 몇 가지 유용한 [로그 검색](log-analytics-log-searches.md) 쿼리입니다.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


*Azure SQL Database에 대한 높은 DTU*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

*Azure SQL Database 탄력적 풀에 대한 높은 DTU*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

Azure SQL 데이터베이스와 탄력적 풀에 대 한 이러한 경고 기반 쿼리 tooalert 특정 임계값에 사용할 수 있습니다. OMS 작업 영역에 대 한 경고 tooconfigure:

#### <a name="tooconfigure-an-alert-for-your-workspace"></a>tooconfigure 작업 영역에 대 한 경고

1. Toohello 이동 [OMS 포털](http://mms.microsoft.com/) 에 로그인 합니다.
2. Hello 솔루션에 대해 구성 된 hello 작업 영역을 엽니다.
3. Hello 개요 페이지에서 클릭 hello **Azure SQL 분석 (미리 보기)** 바둑판식으로 배열입니다.
4. Hello 예제 쿼리 중 하나를 실행 합니다.
5. 로그 검색에서 **경고**를 클릭합니다.  
![검색에서 경고 만들기](./media/log-analytics-azure-sql/create-alert01.png)
6. Hello에 **경고 규칙 추가** 페이지 hello 적절 한 속성을 구성 하 고 원하는 클릭 한 다음 특정 임계값 hello **저장**합니다.  
![경고 규칙 추가](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>Azure SQL 분석 데이터에 대한 작업

예를 들어, 모든 Azure 구독에서 모든 Azure SQL 탄력적 풀에 대 한 toocompare hello DTU 사용률은 수행할 수 있는 hello 가장 유용한 쿼리 중 하나입니다. 데이터베이스 DTU (처리량 단위) 방식으로 toodescribe 제공 Basic, Standard 및 Premium 데이터베이스 및 풀의 성능 수준의 상대적 용량을 hello 합니다. DTU는 CPU, 메모리, 읽기 및 쓰기의 혼합 측정값을 기반으로 합니다. Dtu가 증가 hello 전원 hello 성능 수준 올리기는에서 제공 합니다. 예를 들어 5 DTU의 성능 수준은 1 DTU 성능 수준보다 5배 많은 기능을 제공합니다. 최대 DTU 할당량이 tooeach 서버 및 탄력적인 풀을 적용합니다.

Hello 다음 로그 검색 쿼리를 실행 하 여 하거나 이상의 SQL Azure 탄력적 풀을 활용 하는 경우 쉽게 알 수 있습니다.

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

다음 예제는 hello, 볼 수 있습니다 하나 탄력적 풀에는 거의 100% 사용량이 증가 DTU 거의 사용 했지만 다른 장치입니다. Azure 활동 로그를 사용 하 여 사용자 환경에서 잠재적인 최근 변경 내용을 추가 tootroubleshoot를 조사할 수 있습니다.

![로그 검색 결과 - 높은 사용률](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>참고 항목

- 사용 하 여 [로그 검색](log-analytics-log-searches.md) 로그 분석 tooview에서 Azure SQL 데이터를 자세히 설명 합니다.
- Azure SQL 데이터를 보여 주는 [사용자 고유의 대시보드 만들기](log-analytics-dashboards.md).
- 특정 Azure SQL 이벤트가 발생하는 경우의 [경고 만들기](log-analytics-alerts.md).

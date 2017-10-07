---
title: "Azure 포털 toocreate SQL 데이터베이스 경고 aaaUse | Microsoft Docs"
description: "지정한 hello 조건에 해당할 때 알림 또는 자동화를 트리거할 수 있는 hello 포털 toocreate Azure SQL 데이터베이스 경고를 사용 합니다."
author: aamalvea
manager: jhubbard
editor: 
services: sql-database
documentationcenter: 
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: aamalvea
ms.openlocfilehash: 4e494b130a26c4cdf42445cb49648fce9bf4d300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toocreate-alerts-for-azure-sql-database-and-data-warehouse"></a>Azure 포털 toocreate 경고를 사용 하 여 Azure SQL 데이터베이스 및 데이터 웨어하우스

## <a name="overview"></a>개요
이 문서를 사용 하 여 Azure SQL 데이터베이스 및 데이터 웨어하우스 경고를 tooset Azure 포털을 hello 하는 방법을 보여 줍니다. 이 문서는 또한 경고 기간 설정에 대한 모범 사례를 제공합니다.    

Azure 서비스 또는 Azure 서비스의 이벤트에 대한 모니터링 메트릭을 기반으로 경고를 받을 수 있습니다.

* **메트릭 값** -hello 트리거를 지정 된 메트릭 hello 값 두 방향에서 모두 할당 하는 임계값을 초과할 때 경고 합니다. 즉, 트리거합니다 둘 다 때 hello 조건이 충족 먼저 되 고 다음 나중에 조건 하는 더 이상 충족 합니다.    
* **활동 로그 이벤트** - *모든* 이벤트에 대해 또는 특정 이벤트 수가 발생했을 때만 경고를 트리거할 수 있습니다

표시할 때을 다음 경고 toodo hello를 구성할 수 있습니다.

* 보낼 전자 메일 알림 toohello 서비스 관리자 및 공동 관리자
* 사용자가 지정한 tooadditional 메일 전자 메일을 보냅니다.
* webhook 호출

다음을 통해 경고에 대한 정보를 구성하고 가져올 수 있습니다.

* [Azure 포털](../monitoring-and-diagnostics/insights-alerts-portal.md)
* [PowerShell](../monitoring-and-diagnostics/insights-alerts-powershell.md)
* [명령줄 인터페이스(CLI)](../monitoring-and-diagnostics/insights-alerts-command-line-interface.md)
* [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Azure 포털 hello로 메트릭을에서 경고 규칙 만들기
1. Hello에 [포털](https://portal.azure.com/)hello 리소스 모니터링에 관심이 있는 찾아 선택 합니다.
2. 이 단계는 SQL DB와 탄력적 풀을 사용할 경우와 SQL DW를 사용할 경우에 다릅니다. 

   - **SQL DB & 탄력적 풀만**: 선택 **경고** 또는 **규칙 경고** hello 모니터링 섹션에서. hello 텍스트 및 아이콘 다른 리소스에 대 한 약간 달라질 수 있습니다.  
   
     ![모니터링](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButton.png)
  
   - **SQL DW만**: 선택 **모니터링** hello 일반적인 작업 섹션에서. Hello 클릭 **DWU 사용** 그래프입니다.

     ![일반 작업](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButtonDW.png)

3. 선택 hello **추가 경고** 명령 및 hello 필드를 입력 합니다.
   
    ![Add alert](../monitoring-and-diagnostics/media/insights-alerts-portal/AddDBAlertPage.png)
4. 경고 규칙의 **이름**을 지정하고 **설명**을 선택합니다. 알림 이메일에도 표시되는 항목입니다.
5. 선택 hello **메트릭을** toomonitor, 원하는 다음 선택는 **조건** 및 **임계값** hello 메트릭에 대 한 값입니다. Hello 선택한 **기간** 메트릭을 hello 시간의 규칙 hello 경고 트리거 하기 전에 충족 해야 합니다. 예를 들어 hello 기간 "PT5M"를 사용 하는 경우 경고를 CPU 80% 이상 찾습니다 hello CPU 동안 일관 되 게 위의 80 %5 분 hello 알림을 트리거합니다. Hello 첫 번째 트리거가 발생 한 후 다시 hello CPU 5 분 동안 80% 미만으로 유지 되는 경우를 트리거합니다. CPU 측정 hello 매 1 분 마다 발생합니다.   
6. 확인 **소유자를 전자 메일로 보내기...**  hello 경고 발생 때 관리자와 공동 관리자 toobe 전자 메일로 전송 하려는 경우.
7. 추가 전자 메일 tooreceive 때 hello 알림 경고 발생을 hello에서 추가 **추가 관리자 email(s)** 필드입니다. 여러 전자 메일은 세미콜론(*email@contoso.com;email2@contoso.com*)으로 구분됩니다.
8. Hello 유효한 URI에 put **Webhook** 필드 호출 하려는 경우 경고 발생 hello 때.
9. 선택 **확인** 하면 done toocreate hello 경고 합니다.   

몇 분 안에 hello 경고가 활성 상태 이며 앞에서 설명한 대로 트리거합니다.

## <a name="managing-your-alerts"></a>경고 관리
경고를 만든 후 해당 경고를 선택하여 다음을 수행할 수 있습니다.

* 이전 날짜 hello 메트릭 임계값과 hello hello의 실제 값을 보여 주는 그래프를 봅니다.
* 편집 또는 삭제
* **사용 안 함** 또는 **사용** tootemporarily 중지 하거나 재개 해당 경고에 대 한 알림을 수신 하는 경우.


## <a name="sql-database-alert-values"></a>SQL Database 경고 값

| 리소스 종류 | 메트릭 이름 | 친숙한 이름 | 집계 형식 | 최소 경고 시간 창|
| --- | --- | --- | --- | --- |
| SQL 데이터베이스 | cpu_percent | CPU 비율 | 평균 | 5분 |
| SQL 데이터베이스 | physical_data_read_percent | 데이터 IO 비율 | 평균 | 5분 |
| SQL 데이터베이스 | log_write_percent | 로그 IO 비율 | 평균 | 5분 |
| SQL 데이터베이스 | dtu_consumption_percent | DTU 비율 | 평균 | 5분 |
| SQL 데이터베이스 | 저장소 | 총 데이터베이스 크기 | 최대 | 30분 |
| SQL 데이터베이스 | connection_successful | 성공적인 연결 | 합계 | 10분 |
| SQL 데이터베이스 | connection_failed | 실패한 연결 | 합계 | 10분 |
| SQL 데이터베이스 | blocked_by_firewall | 방화벽에 의해 차단 | 합계 | 10분 |
| SQL 데이터베이스 | 교착 상태 | 교착 상태 | 합계 | 10분 |
| SQL 데이터베이스 | storage_percent | 데이터베이스 크기 비율 | 최대 | 30분 |
| SQL 데이터베이스 | xtp_storage_percent | 메모리 내 OLTP 저장소 백분율(미리 보기) | 평균 | 5분 |
| SQL 데이터베이스 | workers_percent | 작업자 백분율 | 평균 | 5분 |
| SQL 데이터베이스 | sessions_percent | 세션 백분율 | 평균 | 5분 |
| SQL 데이터베이스 | dtu_limit | DTU 제한 | 평균 | 5분 |
| SQL 데이터베이스 | dtu_used | DTU 사용됨 | 평균 | 5분 |
||||||
| 탄력적 풀 | cpu_percent | CPU 비율 | 평균 | 10분 |
| 탄력적 풀 | physical_data_read_percent | 데이터 IO 비율 | 평균 | 10분 |
| 탄력적 풀 | log_write_percent | 로그 IO 비율 | 평균 | 10분 |
| 탄력적 풀 | dtu_consumption_percent | DTU 비율 | 평균 | 10분 |
| 탄력적 풀 | storage_percent | 저장소 비율 | 평균 | 10분 |
| 탄력적 풀 | workers_percent | 작업자 백분율 | 평균 | 10분 |
| 탄력적 풀 | eDTU_limit | eDTU 제한 | 평균 | 10분 |
| 탄력적 풀 | storage_limit | 저장소 제한 | 평균 | 10분 |
| 탄력적 풀 | eDTU_used | eDTU 사용 | 평균 | 10분 |
| 탄력적 풀 | storage_used | 저장소 사용됨 | 평균 | 10분 |
||||||               
| SQL 데이터 웨어하우스 | cpu_percent | CPU 비율 | 평균 | 10분 |
| SQL 데이터 웨어하우스 | physical_data_read_percent | 데이터 IO 비율 | 평균 | 10분 |
| SQL 데이터 웨어하우스 | 저장소 | 총 데이터베이스 크기 | 최대 | 10분 |
| SQL 데이터 웨어하우스 | connection_successful | 성공적인 연결 | 합계 | 10분 |
| SQL 데이터 웨어하우스 | connection_failed | 실패한 연결 | 합계 | 10분 |
| SQL 데이터 웨어하우스 | blocked_by_firewall | 방화벽에 의해 차단 | 합계 | 10분 |
| SQL 데이터 웨어하우스 | service_level_objective | Hello 데이터베이스의 서비스 수준 목표 | 합계 | 10분 |
| SQL 데이터 웨어하우스 | dwu_limit | dwu 제한 | 최대 | 10분 |
| SQL 데이터 웨어하우스 | dwu_consumption_percent | DWU 백분율 | 평균 | 10분 |
| SQL 데이터 웨어하우스 | dwu_used | DWU 사용됨 | 평균 | 10분 |
||||||


## <a name="next-steps"></a>다음 단계
* [Azure 모니터링의 개요를 얻게](../monitoring-and-diagnostics/monitoring-overview.md) hello 형식의 정보를 수집 하 고 모니터링할 수 있습니다.
* [경고에서의 webhook 구성](../monitoring-and-diagnostics/insights-webhooks-alerts.md)에 대해 자세히 알아봅니다.
* 서비스의 상세 고빈도 메트릭을 수집하기 위한 [진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 의 개요를 살펴봅니다.
* 가져오기는 [메트릭 컬렉션의 개요](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake 서비스를 사용 가능 하 고 응답 합니다.

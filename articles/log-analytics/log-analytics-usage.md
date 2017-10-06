---
title: "로그 분석에서 데이터 사용 aaaAnalyze | Microsoft Docs"
description: "로그 분석 tooview 데이터의 양을 toohello 로그 분석 서비스에 전송 되 고 많은 양의 데이터를 보내는 한 문제 해결에 hello 사용 대시보드를 사용 합니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a>Log Analytics에서 데이터 사용 현황 분석
로그 분석에는 컴퓨터 전송 hello 데이터와 hello 다양 한 유형의 전송 되는 데이터 수집 된 데이터 양 hello에 대 한 정보가 포함 됩니다.  사용 하 여 hello **로그 분석 사용량** 데이터 양을 toosee hello 대시보드 toohello 로그 분석 서비스를 전송 합니다. hello 대시보드에 표시 각 솔루션에 의해 수집 되는 데이터 크기 및 데이터의 양을 컴퓨터에 보내집니다.

## <a name="understand-hello-usage-dashboard"></a>Hello 사용 대시보드 이해
hello **로그 분석 사용량** 대시보드는 hello 다음 정보를 표시 합니다.

- 데이터 볼륨
    - (현재 시간 범위에 기반) 시간에 따른 데이터 볼륨
    - 솔루션별 데이터 볼륨
    - 컴퓨터와 연결되지 않은 데이터
- 컴퓨터
    - 데이터를 전송하는 컴퓨터
    - 지난 24시간 동안 데이터가 없는 컴퓨터
- 제품
    - 이해 및 분석 노드
    - Automation 및 제어 노드
    - 보안 노드
- 성능
    - Toocollect 및 인덱스 데이터에 걸린 시간
- 쿼리 목록

![사용량 대시보드](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a>사용 현황 데이터와 toowork
1. 그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com) Azure 구독을 사용 하 여 합니다.
2. Hello에 **허브** 메뉴를 클릭 하 여 **더 많은 서비스** hello 리소스 목록에 입력 하 고 **로그 분석**합니다. 입력을 시작할 때 hello 사용자 입력에 따라 필터를 나열 합니다. **Log Analytics**를 클릭합니다.  
    ![Azure 허브](./media/log-analytics-usage/hub.png)
3. hello **로그 분석** 대시보드 작업 영역 목록이 표시 됩니다. 작업 영역을 선택합니다.
4. Hello에 *작업 영역* 대시보드를 클릭 하 여 **로그 분석 사용량**합니다.
5. Hello에 **로그 분석 사용량** 대시보드를 클릭 하 여 **시간: 마지막 24 시간** toochange hello 시간 간격입니다.  
    ![시간 간격](./media/log-analytics-usage/time.png)
6. 에 관심이 보기 hello 사용 현황 범주 블레이드 영역을 표시 하 합니다. 블레이드를 선택 하 고 다음에 항목을 tooview에서 세부 정보 클릭 [로그 검색](log-analytics-log-searches.md)합니다.  
    ![예제 데이터 사용량 블레이드](./media/log-analytics-usage/blade.png)
7. Hello 로그 검색 대시보드에서 hello 검색에서 반환 되는 hello 결과 검토 합니다.  
    ![예제 사용량 로그 검색](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>데이터 컬렉션이 예상보다 높은 경우 경고를 만듭니다.
이 섹션에서는 설명 방법을 toocreate 경우 경고 합니다.
- 데이터 볼륨이 지정된 크기를 초과합니다.
- 데이터 볼륨은 예측 된 tooexceed 지정된 된 시간입니다.

Log Analytics [경고](log-analytics-alerts-creating.md)는 검색 쿼리를 사용합니다. hello 다음 쿼리에 결과 100 GB 이상 지난 24 시간 동안 hello에 수집 된 데이터의 경우:

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

hello 다음 쿼리는 간단한 수식 toopredict 하루 이상 100GB 데이터의 전송 될 때: 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

다른 데이터 볼륨에서 hello에 변경 hello 100 tooalert tooalert에서 원하는 GB toohello 수를 쿼리 합니다.

에 설명 된 hello 단계를 사용 하 여 [경고 규칙을 생성할](log-analytics-alerts-creating.md#create-an-alert-rule) 예상 보다 더 높은 데이터 수집 될 때 알림을 받으려면 toobe 합니다.

24 시간 동안에서 이상 100GB 데이터의 경우 첫 번째 쿼리에 hello에 대 한 hello 경고를 만들 때 설정 된:
- **이름** 너무*24 시간 동안에서 100 GB 보다 큰 데이터 볼륨*
- **심각도** 너무*경고*
- **검색 쿼리** 너무`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`
- **시간 창** 너무*24 시간 동안*합니다.
- **경고 빈도** toobe 1 시간 이후 hello 사용 현황 데이터는 시간당 한 번만 업데이트 합니다.
- **경고에 따라 생성** toobe *결과의 수*
- **결과 수가** toobe *0 보다 큰*

에 설명 된 hello 단계를 사용 하 여 [동작 tooalert 규칙 추가](log-analytics-alerts-actions.md) hello 경고 규칙에 대 한 전자 메일, webhook, 또는 runbook 작업을 구성 합니다.

두 번째 쿼리에 hello에 대 한 hello 경고를 만드는 것 이상 100GB 데이터의 24 시간 동안에서을 예측할 때 설정 된 경우는:
- **이름** 너무*데이터 볼륨 24 시간 동안에서 100GB 보다 toogreater 필요 합니다.*
- **심각도** 너무*경고*
- **검색 쿼리** 너무`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`
- **시간 창** 너무*3 시간*합니다.
- **경고 빈도** toobe 1 시간 이후 hello 사용 현황 데이터는 시간당 한 번만 업데이트 합니다.
- **경고에 따라 생성** toobe *결과의 수*
- **결과 수가** toobe *0 보다 큰*

경고를 받으면 hello 섹션 tootroubleshoot 사용량이 예상 보다 더 높은 이유를 다음에 hello 단계를 따르세요.

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>사용량이 예상보다 더 높은 원인 해결
hello 사용 대시보드를 사용 하면 tooidentify 이유 사용 현황 (및 따라서 비용)가 예상 보다 더 높습니다.

사용량이 높은 원인은 다음과 같습니다.
- 분석 tooLog 송신할 예상 보다 많은 데이터
- 분석 데이터 tooLog 보내는 예상 보다 더 많은 노드

### <a name="check-if-there-is-more-data-than-expected"></a>예상보다 데이터가 많은지 확인 
대부분의 데이터 toobe 수집 hello 원인을 식별할 수 있도록 hello 사용 현황 페이지의 두 가지 주요 섹션 있습니다.

hello *시간에 따라 데이터 볼륨* 차트 전송 된 데이터의 총 볼륨 hello 보여주며, 전송 하 여 hello 컴퓨터 hello 대부분의 데이터입니다. hello 위쪽 hello 차트가 있습니다 toosee를 남은 시에도 계속 또는 감소 하면 전체 데이터 사용량의 증가 하는 경우. 컴퓨터 hello 목록 hello 대부분의 데이터를 전송 하 여 hello 10 컴퓨터를 표시 합니다.

hello *솔루션 별 데이터 볼륨* 차트에서는 각 솔루션 및 hello 대부분의 데이터를 보내는 hello 솔루션에 의해 전송 되는 데이터 양이 hello를 보여 줍니다. hello 위쪽 hello 차트 hello 전체 시간에 따라 각 솔루션에서 전송 된 데이터 양을 보여 줍니다. 이 정보가 있습니다 tooidentify를 솔루션 이하의 데이터의 데이터를 시간에 따라 해석 동일 hello에 대 한 더 많은 데이터를 보내는 여부. 솔루션의 hello 목록 hello 대부분의 데이터를 보내는 hello 10 솔루션을 보여 줍니다. 

이러한 두 차트는 모든 데이터를 표시합니다. 데이터의 일부는 청구되고 일부는 무료입니다. 검색 페이지 tooinclude hello에 hello 쿼리를 수정 하는 데이터는 청구 가능 에서만 toofocus `IsBillable=true`합니다.  

![데이터 볼륨 차트](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

Hello를 살펴보고 *시간에 따라 데이터 볼륨* 차트입니다. 전송 하는 hello 대부분의 데이터는 특정 컴퓨터에 대 한 데이터 형식과 toosee hello 솔루션 hello hello 컴퓨터 이름을 클릭 합니다. Hello hello 목록에서 첫 번째 컴퓨터의 hello 이름을 클릭 합니다.

다음 스크린 샷 hello에서 hello *로그 관리 / 성능* 데이터 형식의 데이터를 보내고 hello 대부분 hello 컴퓨터에 대 한 합니다. 

![컴퓨터의 데이터 볼륨](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

다음으로 돌아가서 toohello *사용* 대시보드와 hello에 *솔루션 별 데이터 볼륨* 차트입니다. hello는 솔루션에 대 한 대부분의 데이터를 전송 하 여 toosee hello 컴퓨터 hello 목록의 hello 솔루션의 hello 이름을 클릭 합니다. Hello hello 목록에서 첫 번째 솔루션의 hello 이름을 클릭 합니다. 

다음 스크린 샷 hello에서 해당 hello 확인 *acmetomcat* 를 보내 hello hello 로그 관리 솔루션에 대 한 대부분의 데이터입니다.

![솔루션의 데이터 볼륨](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

필요한 경우 솔루션이 나 데이터 형식 내에서 tooidentify 큰 볼륨 추가 분석을 수행 합니다. 예제 쿼리는 다음과 같습니다.

+ **보안** 솔루션
  - `Type=SecurityEvent | measure count() by EventID`
+ **로그 관리** 솔루션
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ **성능** 데이터 형식
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ **이벤트** 데이터 형식
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ **Syslog** 데이터 형식
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ **AzureDiagnostics** 데이터 형식
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

다음 단계 tooreduce hello 볼륨 수집 되는 로그 hello를 사용 합니다.

| 높은 데이터 볼륨의 소스 | 어떻게 tooreduce 데이터 볼륨 |
| -------------------------- | ------------------------- |
| 보안 이벤트            | [일반 또는 최소한의 보안 이벤트](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)를 선택합니다. <br> Hello 보안 감사 정책에만 필요 toocollect 이벤트를 변경 합니다. 특히,에 대 한 hello 필요 toocollect 이벤트를 검토 <br> - [감사 필터링 플랫폼](https://technet.microsoft.com/library/dd772749(WS.10).aspx) <br> - [감사 레지스트리](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)<br> - [감사 파일 시스템](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)<br> - [감사 커널 개체](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)<br> - [감사 핸들 조작](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)<br> - [이동식 저장소 감사](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage) |
| 성능 카운터       | [성능 카운터 구성](log-analytics-data-sources-performance-counters.md)을 다음과 같이 변경합니다. <br> 감소 hello 수집 빈도 <br> - 성능 카운터의 수 감소 |
| 이벤트 로그                 | [이벤트 로그 구성](log-analytics-data-sources-windows-events.md)을 다음과 같이 변경합니다. <br> -이벤트 로그 수집 hello 수가 감소 합니다. <br> - 필수 이벤트 수준만 수집 예를 들어 *정보* 수준 이벤트를 수집하지 않습니다. |
| syslog                     | [syslog 구성](log-analytics-data-sources-syslog.md)을 다음과 같이 변경합니다. <br> -수집 시설 hello 수가 감소 합니다. <br> - 필수 이벤트 수준만 수집 예를 들어 *정보* 및 *디버그* 수준 이벤트를 수집하지 않습니다. |
| AzureDiagnostics           | 다음 작업을 수행하도록 리소스 로그 컬렉션을 변경합니다. <br> -리소스 송신 로그 tooLog 분석 hello 수가 감소 합니다. <br> - 필요한 로그만 수집 |
| Hello 솔루션을 필요로 하지 않는 컴퓨터에서 솔루션 데이터 | 사용 하 여 [솔루션을 대상으로](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect 데이터로 필요한 컴퓨터 그룹에 있습니다. |

### <a name="check-if-there-are-more-nodes-than-expected"></a>예상보다 더 많은 노드가 있는지 확인합니다.
Hello 사용 중인 *(OMS) 노드당* 노드 및 해결책 hello 수에 따라 가격 책정 계층을 청구 합니다. Hello에서 사용 되는 각 제품의 노드 수를 확인할 수 있습니다 *제공* hello 사용 대시보드 섹션.

![사용량 대시보드](./media/log-analytics-usage/log-analytics-usage-offerings.png)

클릭 **모두 표시...**  tooview hello hello 선택한 제공에 대 한 데이터를 전송 하 여 컴퓨터의 전체 목록입니다.

사용 하 여 [솔루션을 대상으로](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect 데이터로 필요한 컴퓨터 그룹에 있습니다.


## <a name="next-steps"></a>다음 단계
* 참조 [로그 분석 검색 로그인](log-analytics-log-searches.md) toolearn toouse hello 언어를 검색 하는 방법입니다. Hello 사용 현황 데이터에서 검색 쿼리 tooperform 추가 분석을 사용할 수 있습니다.
* 에 설명 된 hello 단계를 사용 하 여 [경고 규칙을 생성할](log-analytics-alerts-creating.md#create-an-alert-rule) 충족 될 때 검색 조건 알림을 toobe
* 사용 하 여 [솔루션을 대상으로](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect 데이터로 필요한 그룹의 컴퓨터
* [일반 또는 최소한의 보안 이벤트](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/)를 선택합니다.
* [성능 카운터 구성](log-analytics-data-sources-performance-counters.md)을 변경합니다.
* [이벤트 로그 구성](log-analytics-data-sources-windows-events.md)을 변경합니다.
* [syslog 구성](log-analytics-data-sources-syslog.md)을 변경합니다.

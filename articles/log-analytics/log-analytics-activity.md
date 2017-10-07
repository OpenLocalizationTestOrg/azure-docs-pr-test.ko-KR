---
title: "aaaView Azure 활동 로그 분석을 사용 하 여 기록 | Microsoft Docs"
description: "모든 Azure 구독에서 Azure 활동 로그 솔루션 tooanalyze hello 및 hello Azure 활동 로그 검색을 사용할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 171d0d604d03a5714a9599cc0b448fc5f6471f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="view-azure-activity-logs"></a>Azure 활동 로그 보기

![Azure 활동 로그 기호](./media/log-analytics-activity/activity-log-analytics.png)

활동 로그 분석 솔루션 hello를 사용 하면 분석 하 고 hello 검색 [Azure 활동 로그](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) 모든 Azure 구독에서. hello Azure 활동 로그에는 구독에서 리소스에 수행 하는 hello 작업에 대 한 정보를 제공 하는 로그입니다. hello 활동 로그는 이전에로 알려졌습니다 *감사 로그* 또는 *작업 로그* 구독에 대 한 이벤트를 보고 하기 때문입니다.

Hello 활동 로그를 사용 하 여 hello를 확인할 수 *어떤*, *가*, 및 *때* hello 구독의 리소스에에서 대 한 실행 (PUT, POST, DELETE) 작업이 쓰기에 대 한 합니다. Hello 작업 및 기타 관련 속성의 hello 상태를 이해할 수 있습니다. 읽기 (GET) 작업 또는 작업 hello 클래식 배포 모델을 사용 하는 리소스에 대 한 활동 로그 hello 포함 되지 않습니다.

Azure 활동 로그 tooLog 분석을 연결 하면 다음 작업을 수행할 수 있습니다.

- 미리 정의 된 뷰를 사용 하 여 hello 활동 로그를 분석 합니다.
- 여러 Azure 구독의 활동 로그를 분석하고 검색
- 활동 로그를 90일 이상 보관<sup>1</sup>
- 활동 로그와 다른 Azure 플랫폼 및 응용 프로그램 데이터 간에 상관 관계 지정
- 상태에 따라 집계된 운영 활동 보기
- 각 Azure 서비스에서 발생하는 활동의 추세 보기
- 모든 Azure 리소스에 대한 권한 부여 변경 내용 보고
- 리소스에 영향을 미치는 운영 중단 또는 서비스 상태 문제 식별
- 로그 검색 toocorrelate 사용자 동작, 자동 크기 조정 작업, 권한 부여 변경 및 서비스 상태 tooother 로그 또는 사용자 환경에서 메트릭을 사용 하 여

<sup>1</sup>기본적으로 로그 분석은 유지 Azure 활동 로그를 90 일 동안 hello 무료 계층에 있는 경우에 합니다. 작업 영역 보존 설정이 90일 미만으로 설정된 경우에도 마찬가지입니다. 작업 영역에 있는 보존 90 일 보다 긴 경우 작업 영역 보존 기간이 hello에 대 한 hello 활동 로그 보관 됩니다.

로그 분석 무료로 활동 로그를 수집 하 고 90 일 동안 무료로 hello 로그를 저장 합니다. 90 일 이상에 대 한 로그를 저장 하는 경우 90 일 보다 오래 저장 hello 데이터에 대 한 데이터 보존 요금을 부과할 수 있습니다.

Hello 무료 가격 책정 계층을 사용 하는 경우 작업 로그에는 일일 데이터 소비 tooyour 적용 되지 않습니다.

## <a name="connected-sources"></a>연결된 소스

대부분의 다른 Log Analytics 솔루션과는 달리, 에이전트에서 활동 로그에 대한 데이터를 수집하지 않습니다. Hello 솔루션에서 사용 하는 모든 데이터는 Azure에서 직접 제공 됩니다.

| 연결된 소스 | 지원됨 | 설명 |
| --- | --- | --- |
| [Windows 에이전트](log-analytics-windows-agents.md) | 아니요 | hello 솔루션 Windows 에이전트에서 정보를 수집 하지 않습니다. |
| [Linux 에이전트](log-analytics-linux-agents.md) | 아니요 | hello 솔루션 Linux 에이전트에서 정보를 수집 하지 않습니다. |
| [SCOM 관리 그룹](log-analytics-om-agents.md) | 아니요 | hello 솔루션 연결된 SCOM 관리 그룹의 에이전트에서 정보를 수집 하지 않습니다. |
| [Azure 저장소 계정](log-analytics-azure-storage.md) | 아니요 | hello 솔루션은 Azure 저장소에서 정보를 수집 하지 않습니다. |

## <a name="prerequisites"></a>필수 조건

- Azure 활동 로그 정보 tooaccess Azure 구독이 있어야 합니다.

## <a name="configuration"></a>구성

Hello 단계 tooconfigure hello 활동 로그 분석 솔루션의 작업 영역에 대 한 다음을 수행 합니다.

1. Hello에서 hello 활동 로그 분석 솔루션을 사용 하도록 설정 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.
2. 활동 로그 toogo tooyour 로그 분석 작업 영역을 구성 합니다.
    1. 에 Azure 포털 hello 작업 영역을 선택 하 고 클릭 **Azure 활동 로그**합니다.
    2. 각 구독에 대 한 hello 구독 이름을 클릭 합니다.  
        ![구독 추가](./media/log-analytics-activity/add-subscription.png)
    3. Hello에 *SubscriptionName* 블레이드에서 클릭 **연결**합니다.  
        ![구독 연결](./media/log-analytics-activity/subscription-connect.png)

Hello OMS 포털을 사용 하 여 hello 솔루션을 추가한 경우 hello 다음 타일을 볼 수 있습니다. Azure 구독 tooyour 곗 toohello Azure 포털 tooconnect에에서 로그인 합니다.  
![평가 수행](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여

Hello 활동 로그 분석 솔루션 tooyour 작업 영역에 추가 하면 hello **Azure 활동 로그** 타일 tooyour 개요 대시보드에 추가 됩니다. 이 타일 hello hello 솔루션에는 Azure 구독에 대 한 액세스에 대 한 hello Azure 활동 레코드 수가 개수를 표시 합니다.

![Azure 활동 로그 타일](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a>Azure 활동 로그 보기

Hello 클릭 **Azure 활동 로그** 타일 tooopen hello **Azure 활동 로그** 대시보드 합니다. hello 대시보드는 다음 표에 hello에 hello 블레이드를 포함 합니다. 각 블레이드 hello에 대 한 조건을 블레이드 범위 및 시간 범위를 지정 했는지 일치 too10 항목을 나열 합니다. 클릭 하 여 모든 레코드를 반환 하는 로그 검색을 실행할 수 있습니다 **스크롤하게** hello 블레이드의 또는 hello 블레이드 헤더를 클릭 하 여 hello 맨 아래에 있습니다.

작업 로그 데이터가 나타납니다. *후* 를 구성한 경우 활동 로그 toogo toohello 솔루션, 그 전에 데이터를 볼 수 없습니다.

| 블레이드 | 설명 |
| --- | --- |
| Azure 활동 로그 항목 | 상위 10 개의 작업 호출자 hello 목록이 표시 및 가로 막대형 차트 맨 위로 이동 hello Azure 활동 로그 항목의 선택 된 hello 날짜 범위에 대 한 레코드 합계를 보여 줍니다. 클릭 된 로그 검색에 대 한 가로 막대형 차트 toorun을 hello <code>Type=AzureActivity</code>합니다. 호출자에 게 항목 toorun 해당 항목에 대 한 모든 활동 로그 항목을 반환 하는 로그 검색을 클릭 합니다. |
| 상태별 활동 로그 | 선택한 hello 날짜 범위에 대 한 Azure 활동 로그 상태에 대 한 도넛형 차트를 보여 줍니다. 또한 목록을 hello 상위 10 개 상태 레코드의 목록을 표시합니다. 에 대 한 로그 검색 hello 차트 toorun 클릭 <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>합니다. 상태 항목 toorun 해당 상태 레코드에 대 한 모든 활동 로그 항목을 반환 하는 로그 검색을 클릭 합니다. |
| 리소스별 활동 로그 | Hello 활동 로그를 사용 하 여 리소스의 총 수를 표시 하 고 hello 상위 10 개의 리소스 레코드와 각 리소스에 대 한 계산을 나열 합니다. 에 대 한 로그 검색 hello 전체 영역의 toorun 클릭 <code>Type=AzureActivity &#124; measure count() by Resource</code>, 모든 Azure 리소스를 보여 주는 사용 가능한 toohello 솔루션입니다. 리소스 toorun 해당 리소스에 대 한 모든 작업 레코드를 반환 하는 로그 검색을 클릭 합니다. |
| 리소스 공급자별 활동 로그 | 기록 하 고 hello 상위 10 개의 나열 하는 활동을 생성 하는 리소스 공급자의 총 수 hello 표시 합니다. 에 대 한 로그 검색 hello 전체 영역의 toorun 클릭 <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, 모든 Azure 리소스 공급자를 보여 주는 합니다. 리소스 공급자 toorun hello 공급자에 대 한 모든 작업 레코드를 반환 하는 로그 검색을 클릭 합니다. |

![Azure 활동 로그 대시보드](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a>다음 단계

- 특정 활동이 발생하면 [경고](log-analytics-alerts-creating.md)를 만듭니다.
- 사용 하 여 [로그 검색](log-analytics-log-searches.md) tooview 활동 로그에서 정보를 자세히 설명 합니다.

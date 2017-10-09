---
title: "Azure 저장소 계정이 aaaHow toomonitor | Microsoft Docs"
description: "방법을 사용 하 여 Azure의 저장소 계정 toomonitor hello Azure 포털에 알아봅니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 9a939e0b5db687c1b7b7857399321f681df2056a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a>Hello Azure 포털에서에서 저장소 계정을 모니터링합니다

[Azure 저장소 분석](../storage-analytics.md)은 모든 저장소 서비스에 대한 메트릭과 Blob, 큐 및 테이블에 대한 로그를 제공합니다. Hello를 사용할 수 있습니다 [Azure 포털](https://portal.azure.com) tooconfigure 메트릭 및 로그는 계정에 기록 되 고 메트릭 데이터의 시각적 표현을 제공 하는 차트를 구성 합니다.

> [!NOTE]
> Hello Azure 포털에서에서 모니터링 데이터를 검토할와 관련 된 비용이 있습니다. 자세한 내용은 [저장소 분석 및 청구](/rest/api/storageservices/Storage-Analytics-and-Billing)를 참조하세요.
>
> Azure 파일 저장소는 현재 저장소 분석 메트릭을 지원하지만 아직 로깅을 지원하지 않습니다.
>
> 저장소 계정 복제 형식과 함께 영역 중복 저장소 (ZRS)의 현재 hello 메트릭 또는 로깅 기능을 사용 권한이 없습니다.
> 
> 저장소 분석 및 기타 도구 tooidentify를 사용 하 여 상세 가이드에 대 한 진단, 및 Azure 저장소 관련 문제를 해결 하 고, 참조 [모니터, 진단 및 해결 Microsoft Azure 저장소](../storage-monitoring-diagnosing-troubleshooting.md)합니다.
>

## <a name="configure-monitoring-for-a-storage-account"></a>저장소 계정에 대한 모니터링 구성

1. Hello에 [Azure 포털](https://portal.azure.com)선택, **저장소 계정은**, 다음 hello 저장소 계정 이름 tooopen hello 계정 관리 대시보드.
1. 선택 **진단** hello에 **모니터링** hello 메뉴 블레이드의 섹션입니다.

    ![모니터링 옵션](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. 선택 hello **형식** 각각에 대 한 메트릭 데이터의 **서비스** toomonitor, 원하는 및 hello **보존 정책** hello 데이터에 대 한 합니다. 또한 설정 하 여 모니터링을 해제할 수 있습니다 **상태** 너무**오프**합니다.

    ![모니터링 옵션](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   각 서비스에 사용할 수 있는 메트릭에는 다음 두 가지 유형이 있으며, 둘 다 기본적으로 새 저장소 계정에 사용할 수 있습니다.

   * **집계**: 수신/송신, 가용성, 대기 시간 및 성공 비율과 같은 메트릭을 수집합니다. 이러한 메트릭은 hello blob, 큐, 테이블 및 파일 서비스에 대 한 집계 됩니다.
   * **API 당**:에서 추가 toohello 집계 메트릭을 수집 hello hello Azure 저장소 서비스 API의에서 각 저장소 작업에 대 한 메트릭의 동일한 집합입니다.

   tooset hello 데이터 보존 정책, 이동 hello **보존 (일)** 슬라이더 또는 hello 1 too365에서 데이터 tooretain의 일 수를 입력 합니다. 새 저장소 계정에 대 한 hello 기본값은 7 일입니다. 보존 정책을 tooset 하지 않으려면 0을 입력 합니다. 보존 정책이 없는 경우 tooyou toodelete hello 모니터링 데이터를 표시 됩니다.

   > [!WARNING]
   > 메트릭 데이터를 수동으로 삭제하는 경우 요금이 부과되지만, 오래 된 분석 데이터 (데이터 보존 정책은 다음 보다 오래 된)에 무료로 hello 시스템에서 삭제 됩니다. 사용자 계정에 대 한 tooretain 저장소 분석 데이터를 원하는 시간에 따라 보존 정책을 설정 하는 것이 좋습니다. 자세한 내용은 [저장소 메트릭 사용 시 발생하는 요금](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics)을 참조하세요.
   >

1. Hello 모니터링 구성을 완료 하면 선택 **저장**합니다.

기본 메트릭 집합이 hello 저장소 계정 블레이드: hello 개별 서비스 블레이드 (blob, 큐, 테이블 및 파일)에 차트에 표시 됩니다. 서비스에 대 한 메트릭을 사용 하도록 설정한 후 해당 차트의 데이터 tooappear tooan 시간을 걸릴 수 있습니다. 선택할 수 있습니다 **편집** 모든 메트릭을에 차트 너무[메트릭을 구성할](#how-to-customize-metrics-charts) hello 차트에 표시 됩니다.

설정 하 여 메트릭 수집 및 로깅을 비활성화할 수 **상태** 너무**오프**합니다.

> [!NOTE]
> Azure 저장소를 사용 하 여 [테이블 저장소](../common/storage-introduction.md#table-storage) toostore hello 메트릭이 저장소 계정 및 계정에는 테이블의 저장소 hello 메트릭. 자세한 내용은 다음을 참조하세요. [메트릭 저장 방법](../common/storage-analytics.md#how-metrics-are-stored).
>

## <a name="customize-metrics-charts"></a>메트릭 차트 사용자 지정

메트릭 차트에 다음 프로시저 toochoose hello는 저장소 메트릭 tooview을 사용 합니다. 

1. Hello Azure 포털에에서 저장소 메트릭 차트를 표시 하 여 시작 합니다. Hello에 차트를 찾을 수 있습니다 **저장소 계정 블레이드** 및 hello **메트릭** 블레이드는 개별 서비스 서비스 (blob, 큐, 테이블, 파일)에 대 한 합니다.

   이 예제에서는 협력 hello에 나타나는 차트를 수행 하는 hello **저장소 계정 블레이드**:

   ![Azure Portal에서 차트 선택](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. 다음으로 hello 차트 tooopen hello 내에서 아무 곳 이나 클릭 **메트릭을** 블레이드입니다. 선택 **차트 편집** tooopen hello **차트 편집** 블레이드입니다.

   ![차트 블레이드의 차트 편집 단추](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. Hello에 **차트 편집** 블레이드, 선택 hello **시간 범위** hello 차트 및 hello hello 메트릭 toodisplay의 **서비스** (blob, 큐, 테이블, 파일) 인 메트릭을 toodisplay 합니다. 여기의 주 메트릭 hello blob 서비스에 대 한 지난 toodisplay hello 선택:

   ![Hello 차트 편집 블레이드에서 시간 범위 및 서비스 선택](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. 선택 hello 개별 **메트릭** hello 차트에 표시 되는 like, 클릭 **확인**합니다. 예를 들어, 여기에서는 선택한 toodisplay hello *ContainerCount* 및 *ObjectCount* 메트릭:

   ![차트 편집 블레이드의 개별 메트릭 선택](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

차트 설정 hello 수집, 집계 또는 모니터링 hello 저장소 계정에는 데이터 저장소에 영향을 줄만 메트릭 데이터 보기를 hello 되지 않습니다.

### <a name="metrics-availability-in-charts"></a>차트의 메트릭 가용성

hello 드롭다운 목록에서에서 선택한 서비스에 기반 하 여 사용 가능한 메트릭 변경의 hello 목록 및 편집 하 고 있는 hello 차트의 hello 단위 유형입니다. 예를 들어 단위를 백분율로 표시하는 차트를 편집하는 경우에만 *PercentNetworkError* 및 *PercentThrottlingError*와 같은 백분율 메트릭을 선택할 수 있습니다.

![Hello Azure 포털에서에서 요청 오류 백분율 차트](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a>메트릭 해상도

hello 메트릭 진단에서 선택한 계정에 대해 사용할 수 있는 hello 메트릭의 hello 해상도를 결정 합니다.

* **집계** 모니터링은 수신/송신, 가용성, 대기 시간 및 성공 비율과 같은 메트릭을 제공합니다. 이러한 메트릭은 hello blob, 테이블, 파일 및 큐 서비스에서 집계 됩니다.
* **API 당** 더욱 세밀 하 게 해결 방법을 제공, 개별 저장소 작업에 사용할 수 있는 메트릭을 사용 하 여 또한 toohello 서비스 수준 집계 합니다.

## <a name="configure-metrics-alerts"></a>메트릭 경고 구성

경고 toonotify를 만들 수 있습니다 때 저장소 리소스 메트릭에 대 한 임계값에 도달 했습니다.

1. tooopen hello **경고 규칙 블레이드**, toohello 아래로 스크롤하여 **모니터링** hello 섹션 **메뉴 블레이드** 선택 **규칙 경고**합니다.
1. 선택 **추가 경고** tooopen hello **경고 규칙 추가** 블레이드
1. 선택 된 **리소스** (blob, 파일, 큐, 테이블)에서 드롭 다운 hello 및 입력는 **이름** 및 **설명** 새 경고 규칙에 대 한 합니다.
1. 선택 hello **메트릭을** 하려는 tooadd 경고를 경고 **조건**, 및 **임계값**합니다. hello 임계값 단위 형식 변경 hello 메트릭에 따라을 선택 했습니다. 예를 들어, "count" hello 단위 형식입니다. *ContainerCount*, hello에 대 한 hello 단위 동안 *PercentNetworkError* 메트릭을 백분율로 표시 됩니다.
1. 선택 hello **기간**합니다. 에 도달 하거나 초과 하는 메트릭을 트리거에서 hello 기간 경고 임계값을 hello 합니다.
1. (선택 사항) **전자 메일** 및 **웹후크** 알림을 구성합니다. 웹후크에 대한 자세한 내용은 [Azure 메트릭 경고에 대한 웹후크 구성](../../monitoring-and-diagnostics/insights-webhooks-alerts.md)을 참조하세요. Webhook 또는 전자 메일 알림을 구성 하지 않으면 경고는 hello Azure 포털에만 표시 됩니다.

![Hello Azure 포털의에서 경고 규칙 추가' 블레이드](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a>메트릭 차트 toohello 포털 대시보드를 추가 합니다.

저장소 계정 tooyour 포털 대시보드에서 중 하나에 대 한 Azure 저장소 메트릭 차트를 추가할 수 있습니다.

1. 선택 클릭 **대시보드 편집** hello에 대시보드를 보는 동안 [Azure 포털](https://portal.azure.com)합니다.
1. Hello에 **타일 갤러리**선택, **찾기 바둑판식으로 표시 하 여** > **형식**합니다.
1. **유형** > **저장소 계정**을 차례로 선택합니다.
1. **리소스**, hello 저장소 계정을 tooadd toohello 대시보드 해당 메트릭을 선택 합니다.
1. **범주** > **모니터링**을 차례로 선택합니다.
1. 끌어서 놓기 hello 차트에 표시 하려는 hello 메트릭에 대 한 대시보드 타일입니다. Hello 대시보드에 표시 되는 모든 메트릭 선택에 대 한 반복 합니다. 다음 이미지는 hello, hello "Blob-총 요청" 차트 예를 들어, 강조 표시 되어 있지만 모든 hello 차트를 대시보드에 배치에 사용할 수 있습니다.

   ![Azure Portal의 타일 갤러리](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. 선택 **사용자 지정 작업은 수행** 추가 차트 완료 되 면 hello 대시보드의 hello 맨 위 근처에 있습니다.

차트 tooyour 대시보드를 추가 하면 추가로 사용자 지정할 수 있습니다 하에 설명 된 대로 [차트를 사용자 지정](#how-to-customize-metrics-charts)합니다.

## <a name="configure-logging"></a>로깅 구성

Azure 저장소 toosave 진단 로그에 대 한 읽기, 쓰기 및 삭제 hello blob, 테이블 및 큐 서비스에 대 한 요청을 지시할 수 있습니다. hello 데이터 보존 정책을 설정 하면에 toothese 로그도 적용 됩니다.

> [!NOTE]
> Azure 파일 저장소는 현재 저장소 분석 메트릭을 지원하지만 아직 로깅을 지원하지 않습니다.
>

1. Hello에 [Azure 포털](https://portal.azure.com)선택, **저장소 계정은**, 블레이드의 hello 저장소 계정 tooopen hello 저장소 계정 hello 이름을 차례로 합니다.
1. 선택 **진단** hello에 **모니터링** hello 메뉴 블레이드의 섹션입니다.

    ![진단 메뉴 항목 모니터링 아래의 hello Azure 포털에서에서입니다.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. 확인 **상태** 너무 설정**에**, 및 선택 hello **서비스** 하려는 tooenable 로깅.

    ![Hello Azure 포털에서에서 로깅 구성 합니다.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. **Save**를 클릭합니다.

hello 진단 로그는 저장소 계정의 $logs 라는 blob 컨테이너에 저장 됩니다. Hello와 같은 저장소 탐색기를 사용 하 여 hello 로그 데이터를 볼 수 있습니다 [Microsoft 저장소 탐색기](http://storageexplorer.com), hello 저장소 클라이언트 라이브러리 또는 PowerShell을 사용 하 여 프로그래밍 방식으로 또는 합니다.

Hello $logs 컨테이너에 액세스 하는 방법에 대 한 정보를 참조 하십시오. [저장소 로깅을 사용 하도록 설정 및 로그 데이터에 액세스](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data)합니다.

## <a name="next-steps"></a>다음 단계

* 저장소 분석의 [메트릭, 로깅 및 청구](../storage-analytics.md)에 대해 자세히 알아봅니다.
* PowerShell 및 프로그래밍 방식으로 C#을 사용하여 [Azure Storage 메트릭 사용 및 메트릭 데이터 보기](../storage-enable-and-view-metrics.md)를 수행합니다.

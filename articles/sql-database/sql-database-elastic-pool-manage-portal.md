---
title: "Azure Portal: SQL Database 탄력적 풀 만들기 및 관리 | Microsoft Docs"
description: "Toouse hello Azure 포털 및 SQL 데이터베이스의 기본 제공 인텔리전스 toomanage, 모니터 및 적정 크기로 확장 가능한 탄력적 풀 toooptimize 데이터베이스 성능 및 비용 관리 방법에 대해 알아봅니다."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a>만들기 및 Azure 포털 hello로 탄력적 풀 관리
이 항목에서는 toocreate 하 고 확장 가능한 관리 [탄력적 풀](sql-database-elastic-pool.md) hello Azure 포털을 사용 합니다. 또한 생성 하 고 있는 Azure 탄력적 풀 관리 수 [PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API hello 또는 [C#](sql-database-elastic-pool-manage-csharp.md)합니다. [Transact-SQL](sql-database-elastic-pool-manage-tsql.md)을 사용하여 탄력적 풀을 만들고 여기에 데이터베이스를 넣거나 뺄 수도 있습니다.

## <a name="create-an-elastic-pool"></a>탄력적 풀 만들기 

두 가지 방법으로 탄력적 풀을 만들 수 있습니다. Hello 풀 설치 프로그램을 시작 하 든 hello 서비스에서 권장을 알고 있는 경우 처음부터이 수행할 수 있습니다. SQL 데이터베이스에 더 비용 효율적 사용 원격 분석 데이터베이스에 대 한 지난 hello에 근거 하는 경우 탄력적 풀 설치 프로그램을 권장 하는 기본 제공 인텔리전스 있습니다.

서버에서 여러 풀을 만들 수 있지만 hello에 서로 다른 서버에서 데이터베이스를 추가할 수 없습니다 동일한 풀입니다. 

> [!NOTE]
> 탄력적 풀은 현재 미리 보기 상태인 인도 서부를 제외한 모든 Azure 지역에서 일반 공급(GA) 상태입니다.  이 영역에서 탄력적 풀의 GA는 가능한 한 빨리 수행될 예정입니다.
>

### <a name="step-1-create-an-elastic-pool"></a>1단계: 탄력적 풀 만들기

기존 탄력적 풀을 만들어 **서버** hello 포털에서 블레이드는 hello 가장 쉬운 방법은 toomove 기존 데이터베이스를 탄력적 풀으로 합니다.

> [!NOTE]
> 검색 하 여 탄력적 풀을 만들 수도 있습니다 **SQL 탄력적인 풀** hello에 **마켓플레이스** 클릭 하거나 **+ 추가** hello에 **SQL 탄력적 풀**블레이드를 탐색 합니다. 워크플로 프로 비전 하는이 풀을 통해 기존 또는 새 서버 수 toospecify 됩니다.
>
>

1. Hello에 [Azure 포털](http://portal.azure.com/), 클릭 **더 많은 서비스**  **>**  **SQL server**, 다음 hello를 포함 하는 hello 서버를 클릭 하 고 데이터베이스 tooadd tooan 탄력적 풀에서 사용할 수 있는 권한
2. **새 풀**을 클릭합니다.

    ![풀 tooa 서버 추가](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **또는**

    표시 될 수 있습니다 있습니다 한다는 메시지가 hello 서버에 대 한 탄력적 풀 권장 됩니다. Hello 메시지 toosee hello 권장 되는 기록 데이터베이스 사용량 원격 분석에 따라 풀을 클릭 한 다음 자세한 내용을 보려면 hello 계층 toosee를 클릭 하 고 hello 풀을 사용자 지정 합니다. 참조 [풀 권장 사항을 이해](#understand-elastic-pool-recommendations) 이 항목 뒷부분의 hello 권장 사항 생성 되는 방법에 대 한 합니다.

    ![권장되는 풀](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. hello **탄력적 풀** 블레이드 표시 되는 풀에 대해 hello 설정을 지정 하는 합니다. 클릭 한 경우 **새 풀** hello 가격 책정 계층은 hello 이전 단계에서 **표준** 데이터베이스가 없고 하 고 기본적으로 선택 되어 있습니다. 빈 풀을 만들거나 hello 풀으로 해당 서버 toomove에서 기존 데이터베이스의 집합을 지정할 수 있습니다. 권장된 풀을 만드는 경우 hello 가격 책정 계층, 성능 설정 및 데이터베이스의 목록을 미리 채워져 있습니다, 좋지만 변경할 수 있습니다.

    ![탄력적 풀 구성](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. Hello 탄력적 풀에 대 한 이름을 지정 하거나 hello 기본값으로 그대로 둡니다.

### <a name="step-2-choose-a-pricing-tier"></a>2단계: 가격 책정 계층 선택

hello 풀의 가격 책정 계층이 결정 hello hello 그룹 및 hello 최대 수 (최대 eDTU) Edtu 및 저장소 (Gb) 사용 가능한 tooeach 데이터베이스의 사용 가능한 toohello elastics 기능 합니다. 자세한 내용은 서비스 계층을 참조하세요.

hello toochange hello 풀에 대 한 가격 책정 계층을 클릭 **가격 책정 계층**, 가격 책정 계층을 하 고 클릭 hello 클릭 **선택**합니다.

> [!IMPORTANT]
> Hello 가격 책정 계층을 선택 하 고 클릭 하 여 변경 내용을 적용 한 후 **확인** hello 마지막 단계에서 가격 책정 계층 hello 풀의 수 toochange hello 됩니다. toochange hello 기존 탄력적 풀의 가격 책정 계층을 hello 원하는 가격 책정 계층에서 탄력적 풀을 만들거나 hello 데이터베이스 toothis 새 풀을 마이그레이션합니다.
>

![가격 책정 계층 선택](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a>3 단계: hello 풀 구성

가격 책정 계층 hello를 설정한 후 데이터베이스, 집합 풀 Edtu 및 저장소 (풀 Gb)를 추가 하 고 hello 풀의 hello min 및 max Edtu elastics hello에 대 한 설정 구성 풀을 클릭 합니다.

1. **풀 구성**
2. Tooadd toohello 풀에서 사용할 hello 데이터베이스를 선택 합니다. Hello 풀을 만드는 동안이 단계는 선택 사항입니다. Hello 풀이 만들어진 후에 데이터베이스를 추가할 수 있습니다.
    tooadd 데이터베이스 클릭 **데이터베이스 추가**, hello 데이터베이스 tooadd를 원하고 hello를 클릭 한 다음 클릭 **선택** 단추입니다.

    ![데이터베이스 추가](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    사용 하는 hello 데이터베이스 데이터베이스의 기록 사용 만큼 원격 분석이 충분 경우 hello **예상 eDTU 및 GB 사용량** 그래프 및 hello **실제 eDTU 사용량** 가로 막대형 차트 업데이트 toohelp 구성 확인 의사 결정 합니다. 또한 hello 서비스가 제공할 수 있습니다 권장 메시지 toohelp 풀 hello 적정 크기로 있습니다. [동적 권장 사항](#understand-elastic-pool-recommendations)을 참조하세요.

3. Hello에 hello 컨트롤을 사용 하 여 **풀 구성** tooexplore 설정 페이지 및 프로그램 풀을 구성 합니다. 각 서비스 계층의 제한에 대한 자세한 내용은 [탄력적 풀 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하고 적정한 탄력적 풀의 크기에 대한 자세한 지침은 [탄력적 풀에 대한 가격 및 성능 고려 사항](sql-database-elastic-pool.md)을 참조하세요. 풀 설정에 대한 자세한 내용은 [탄력적 풀 속성](sql-database-elastic-pool.md#database-properties-for-pooled-databases)을 참조하세요.

    ![탄력적 풀 구성](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. 클릭 **선택** hello에 **풀 구성** 설정을 변경한 후 블레이드 합니다.
5. 클릭 **확인** toocreate hello 풀입니다.

## <a name="understand-elastic-pool-recommendations"></a>탄력적 풀 권장 사항 이해

hello SQL 데이터베이스 서비스는 사용 현황을 평가 하 고 단일 데이터베이스를 사용 하 여 보다 비용 효율성이 되었을 때 하나 이상의 풀은 것이 좋습니다. 각 권장 사항은 hello 풀에 가장 잘 맞는 hello 서버 데이터베이스의 고유 하위 집합으로 구성 됩니다.

![권장되는 풀](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

hello 풀 권장이 됩니다.

- Hello 풀 (Basic, Standard, Premium 또는 프리미엄 RS)에 대 한 가격 책정 계층
- 적절한 **풀 eDTU** (풀당 최대 eDTU)
- hello **최대 eDTU** 및 **eDTU Min** 데이터베이스당
- hello hello 풀에 대 한 권장된 데이터베이스 목록

> [!IMPORTANT]
> hello 서비스 고려 hello 원격 분석의 지난 30 일 동안 풀 권장할 때 합니다. 탄력적 풀에 대 한 대상으로 간주 하는 데이터베이스 toobe에 대 한 일 이상 있어야 합니다. 이미 탄력적 풀에 있는 데이터베이스는 탄력적 풀 권장 사항에 대한 후보로 간주되지 않습니다.
>

hello 서비스의 리소스 수요를 평가 및 단일 이동 hello의 비용 효율 데이터베이스 각 서비스 계층에서의 hello 풀에 동일한 계층입니다. 예를 들어 서버의 모든 Standard 데이터베이스는 표준 탄력적 풀에 적합한지 평가됩니다. 즉, hello 서비스 계층 간 권장 사항을 표준 데이터베이스는 프리미엄 풀으로 이동 하는 등을 만들지 않습니다.

데이터베이스 toohello 풀을 추가한 다음 권장 사항은 동적으로 생성 되 hello 선택한 hello 데이터베이스의 기존 사용량 기반 합니다. 이러한 권장 hello eDTU 및 GB 사용 현황 차트에서 고 hello hello 맨 위의 권장 사항 배너에 표시 됩니다 **풀 구성** 블레이드입니다. 이러한 권장 사항은 의도 한 tooassist 특정 데이터베이스에 대해 최적화 된 탄력적 풀을 만드는 있습니다.

![동적 권장 사항](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a>탄력적 풀 관리 및 모니터링

Azure 포털 toomonitor hello를 사용 하 고 탄력적 풀 및 hello 풀의 hello 데이터베이스를 관리할 수 있습니다. Hello 포털에서 탄력적 풀과 해당 풀 내의 hello 데이터베이스의 hello 사용률을 모니터링할 수 있습니다. 변경 내용 집합이 tooyour 탄력적 풀을 확인 하 고 모든 변경 내용을 hello 동일 제출할 수도 있습니다 시간입니다. 이러한 변경 내용에는 데이터베이스 추가 또는 제거, 탄력적 풀 설정 변경, 데이터베이스 설정 변경이 포함됩니다.

다음 그래픽 hello 예제 탄력적 풀을 보여 줍니다. hello 보기에는 다음이 포함 됩니다.

*  Hello 탄력적 풀과 hello 풀에 포함 된 hello 데이터베이스의 리소스 사용 모니터링에 대 한 차트를 제공 해야 합니다.
*  hello **구성** 풀 단추 toomake toohello 탄력적 풀을 변경 합니다.
*  hello **데이터베이스 만들기** 데이터베이스를 만드는 단추 toohello 현재 탄력적 풀을 추가 합니다.
*  목록의 모든 데이터베이스에 대해 Transact SQL 스크립트를 실행하여 많은 데이터베이스를 관리하는 데 도움이 되는 탄력적 작업

![풀 보기][2]

해당 리소스 사용률 tooa 특정 풀 toosee를 이동할 수 있습니다. 기본적으로 hello 풀 지난 1 시간 동안 hello에 대 한 구성된 tooshow 저장소 및 eDTU 사용량은입니다. hello 차트에는 다양 한 시간 창에 대해 구성 된 tooshow 가지 다른 메트릭으로 수 있습니다.

1. 와 탄력적인 풀 toowork를 선택 합니다.
2. **탄력적 풀 모니터링**에는 차트 레이블이 지정된 **리소스 사용률**이 있습니다. Hello 차트를 클릭 합니다.

    ![탄력적 풀 모니터링][3]

    hello **메트릭을** 메트릭 hello 지정 된 기간 동안 지정 된 hello에 대 한 자세히 보기를 보여 주는, 블레이드를 엽니다.   

    ![메트릭 블레이드][9]

### <a name="toocustomize-hello-chart-display"></a>toocustomize hello 차트 표시

CPU 비율, 데이터 IO 백분율 및 사용 되는 로그 IO 백분율 등 기타 메트릭을 hello 차트 및 hello 메트릭 블레이드 toodisplay 편집할 수 있습니다.

1. Hello 메트릭 블레이드 클릭 **편집**합니다.

    ![편집 클릭][6]

2. Hello에 **차트 편집** 블레이드에서 (지난 시간을 오늘 또는 지난 주), 시간 범위를 선택 하거나 클릭 **사용자 지정** tooselect 날짜 범위에 속하는 hello 지난 2 주입니다. Hello 차트 종류 (가로 막대형 또는 꺾은선형)를 선택 하 고 hello 리소스 toomonitor를 선택 합니다.

   > [!Note]
   > 동일한 hello에 hello 동일한 측정 단위는 hello에 표시 될 수 있는 메트릭 차트에 시간입니다. 예를 들어 "eDTU percentage"를 선택 하는 경우 선택할 수 있습니다만 기타 메트릭을 (백분율)으로 hello 측정 단위입니다.
   >

    ![편집 클릭](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. 그런 후 **OK**를 클릭합니다.

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>탄력적 풀의 데이터베이스 관리 및 모니터링

문제 발생 가능성에 대한 개별 데이터베이스를 모니터링할 수도 있습니다.

1. **탄력적 데이터베이스 모니터링**에는 다섯 개의 데이터베이스에 대한 메트릭을 표시하는 차트가 있습니다. 기본적으로 hello 차트 표시 hello 상위 5 데이터베이스 hello 풀의 평균 eDTU 사용량 hello에 의해 지난 시간 합니다. Hello 차트를 클릭 합니다.

    ![탄력적 풀 모니터링][4]

2. hello **데이터베이스 리소스 사용률** 블레이드 나타납니다. Hello 데이터베이스 사용 hello 풀에 대 한 자세히 보기를 제공합니다. Hello 블레이드의 hello 아래쪽 표에 hello를 사용 하 선택할 수 있습니다 데이터베이스가 hello 풀 toodisplay에 hello 차트 (too5 데이터베이스)를 사용 합니다. Hello 메트릭 및 시간 창을 클릭 하 여 hello 차트에 표시를 사용자 지정할 수도 있습니다 **차트 편집**합니다.

    ![데이터베이스 리소스 사용률 블레이드][8]

### <a name="toocustomize-hello-view"></a>toocustomize hello 보기

1. Hello에 **리소스 사용률이 데이터베이스** 블레이드에서 클릭 **차트 편집**합니다.

    ![차트 편집 클릭](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. Hello에 **편집** 블레이드에서 차트, 시간 범위 (지난 시간, 지난 24 시간)를 선택 하거나 클릭 **사용자 지정** 지난 2 주 toodisplay hello에 다른 하루 tooselect 합니다.

    ![사용자 지정 클릭](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. Hello 클릭 **하 여 데이터베이스를 비교할** 드롭다운 tooselect 다른 메트릭 toouse 데이터베이스를 비교 하는 경우.

    ![Hello 차트 편집](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect 데이터베이스 toomonitor

Hello에 hello 데이터베이스 목록에서 **데이터베이스 리소스 사용률** 블레이드에서 hello 페이지 hello 목록을 조회 하거나 데이터베이스의 hello 이름에 입력 하 여 특정 데이터베이스를 찾을 수 있습니다. Hello 확인란 tooselect hello 데이터베이스를 사용 합니다.

![데이터베이스 toomonitor 검색][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a>경고 tooan 탄력적 풀 리소스 추가

탄력적 풀 hello 설정 하는 사용 임계값에 도달 하면 전자 메일 문자열 tooURL 끝점 toopeople 또는 경고를 전송 하는 규칙 tooan 탄력적 풀을 추가할 수 있습니다.

**tooadd 경고 tooany 리소스:**

1. Hello 클릭 **리소스 사용률** 차트 tooopen hello **메트릭을** 블레이드에서 클릭 **추가 경고**, hello에 hello 정보 입력 **경고를 추가 규칙** 블레이드 (**리소스** 작업할 때 toobe hello 풀을 자동으로 설정 됩니다).
2. 입력 **이름** 및 **설명** hello 경고 tooyou 및 hello 받는 사람을 식별 하 합니다.
3. 선택 된 **메트릭을** tooalert hello 목록에서 원하는 합니다.

    동적으로 hello 차트 메트릭 해당 toohelp에 대 한 리소스 사용률 표시 임계값을 선택 합니다.

4. **조건**(보다 큼, 보다 작음 등) 및 **임계값**을 선택합니다.
5. 선택 된 **기간** 메트릭을 hello 시간의 규칙 hello 경고 트리거 하기 전에 충족 해야 합니다.
6. **확인**을 클릭합니다.

자세한 내용은 [Azure Portal에서 SQL Database 경고 만들기](sql-database-insights-alerts-portal.md)를 참조하세요.

## <a name="move-a-database-into-an-elastic-pool"></a>탄력적 풀로 데이터베이스 이동

기존 풀에서 데이터베이스를 제거하거나 추가할 수 있습니다. hello 데이터베이스가 다른 풀 있을 수 있습니다. 그러나만 추가할 수 있습니다는에 hello 동일 데이터베이스 논리 서버입니다.

1. Hello 풀에 대 한 hello 블레이드에서 아래 **탄력적 데이터베이스** 클릭 **풀 구성**합니다.

    ![풀 구성 클릭][1]

2. Hello에 **풀 구성** 블레이드에서 클릭 **toopool 추가**합니다.

    ![추가 toopool 클릭](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. Hello에 **데이터베이스를 추가할** 블레이드, 선택 hello 데이터베이스 또는 데이터베이스 tooadd toohello 풀입니다. 그런 다음 **선택**을 클릭합니다.

    ![데이터베이스 tooadd 선택](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    hello **풀 구성** 블레이드 목록 hello toobe 너무 설정 상태와 함께 추가 하면 선택한 데이터베이스는 이제**보류 중인**합니다.

    ![보류 중인 풀 추가](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. Hello에 **구성 풀 블레이드에서**, 클릭 **저장**합니다.

    ![저장을 클릭합니다.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>탄력적 풀 외부로 데이터베이스 이동

1. Hello에 **풀 구성** 블레이드, 선택 hello 데이터베이스 또는 데이터베이스 tooremove 합니다.

    ![데이터베이스 나열](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. **풀에서 제거**를 클릭합니다.

    ![데이터베이스 나열](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    hello **풀 구성** 블레이드 목록 hello 너무 설정 상태가 제거할 toobe 선택한 데이터베이스는 이제**보류 중인**합니다.

    ![데이터베이스 추가 및 제거 미리 보기](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. Hello에 **구성 풀 블레이드에서**, 클릭 **저장**합니다.

    ![저장을 클릭합니다.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>탄력적 풀의 성능 설정 변경

탄력적 풀의 hello 리소스 사용률을 모니터링 하면서 약간씩 조정 필요한 경우도 있습니다. 아마 hello 풀 hello 성능이 나 저장소 제한 변경을 해야합니다. Hello 풀에서 toochange hello 데이터베이스 설정을 원하는 것 같습니다. 모든 시간 tooget hello 적절 한 성능 및 비용에 hello 풀의 hello 설정을 변경할 수 있습니다. 자세한 내용은 [탄력적 풀을 사용해야 하는 경우](sql-database-elastic-pool.md)를 참조하세요.

toochange hello Edtu 또는 저장소 풀 및 데이터베이스당 Edtu 당 제한 됩니다.

1. 열기 hello **풀 구성** 블레이드입니다.

    아래 **탄력적 풀 설정**, 풀 설정을 하거나 슬라이더 toochange hello를 사용 합니다.

    ![탄력적 풀 리소스 사용률](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. Hello 설정이 변경 되 면 hello 표시 hello hello 변경의 월별 비용을 예상 합니다.

    ![탄력적 풀 및 새 월별 비용 업데이트](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>탄력적 풀 작업의 대기 시간
* 5 분 이내에 완료 데이터베이스 마다 데이터베이스 또는 최대 Edtu 당 hello 최소 Edtu를 일반적으로 변경 합니다.
* Hello Edtu 풀 당 변경 hello hello 풀의 모든 데이터베이스에 사용 되는 공간의 총 금액에 따라 달라 집니다. 변경 시간은 100GB당 평균 90분 이하입니다. 예를 들어 hello 총 공간에서 사용 하는 경우 hello 풀의 모든 데이터베이스는 200GB, 다음 hello 필요한 hello 풀 eDTU 풀 당 변경에 대 한 대기 시간은 3 시간 이내입니다.

## <a name="next-steps"></a>다음 단계

- 어떤 탄력적 풀 참조 이면 toounderstand [SQL 데이터베이스 탄력적 풀](sql-database-elastic-pool.md)합니다.
- 탄력적 풀 사용에 대한 지침을 보려면 [탄력적 풀의 가격 및 성능 고려 사항](sql-database-elastic-pool.md)을 참조하세요.
- 임의 개수의 hello 풀의 데이터베이스에 대해 toouse 탄력적 작업 toorun Transact SQL 스크립트 참조 [탄력적 작업 개요](sql-database-elastic-jobs-overview.md)합니다.
- hello 풀의 데이터베이스 수 전체 tooquery 참조 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)합니다.
- 트랜잭션에 대 한 여러 hello 풀에 데이터베이스 참조 [탄력적 트랜잭션을](sql-database-elastic-transactions-overview.md)합니다.


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png

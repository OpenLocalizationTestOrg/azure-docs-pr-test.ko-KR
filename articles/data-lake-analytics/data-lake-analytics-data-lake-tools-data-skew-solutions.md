---
title: "Visual Studio 용 Azure 데이터 레이크 도구를 사용 하 여 데이터 불일치가 문제 aaaResolve | Microsoft Docs"
description: "Azure Data Lake Tools for Visual Studio를 사용하여 데이터 기울이기 문제에 대한 잠재적인 해결 방법을 마련합니다."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a>Azure Data Lake Tools for Visual Studio를 사용하여 데이터 기울이기 문제 해결

## <a name="what-is-data-skew"></a>데이터 기울이기란?

간단히 말해 데이터 기울이기는 지나치게 많은 값입니다. 할당 했는지 50 세금 examiners 각 미국 주에 대 한 하나의 검사기 tooaudit 세금 반환 한다고 가정 합니다. hello 와이오밍 검사기 hello 채우기 있습니다 작습니다 있기 때문에 거의 toodo를 포함 합니다. 그러나 캘리포니아에 hello 검사기 유지 되 사용률이 매우 높은 hello 상태가 대형 채우기 때문입니다.
    ![데이터 기울이기 문제 예](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)

이 시나리오에서 hello 데이터는 전체에 고르게 분포 모든 세금 examiners 일부 examiners 다른 항목 보다 더 작업 해야 한다는 의미입니다. 사용자 고유의 작업에서 자주 hello 세금 검사기 예제 여기는 경우 발생합니다. 꼭 짓 점을 보다 기술적인 측면에서 작동 하 고 다른 결국 속도 낮추고 전체 작업 hello 이상 hello 꼭 짓 점에 대해 수행 하는 상황의 피어 보다 훨씬 더 많은 데이터를 가져옵니다. 나쁜 이란 hello 작업이 실패, 예를 들어 꼭 짓 점이 있을 수 있으므로 런타임 5 시간 제한 및 6 GB 메모리 제한입니다.

## <a name="resolving-data-skew-problems"></a>데이터 기울이기 문제 해결

Azure Data Lake Tools for Visual Studio는 작업에 데이터 기울이기 문제가 있는지 확인할 수 있습니다. 문제가 있으면이 섹션의 hello 솔루션을 시도 하 여 해결할 수 있습니다.

## <a name="solution-1-improve-table-partitioning"></a>해결 방법 1: 테이블 분할 향상

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a>옵션 1: 필터 hello 왜곡 키 값을 미리

비즈니스 논리에는 영향을 주지 않는 미리 hello 더 높은 주파수 값을 필터링 할 수 있습니다. 예를 들어 000-000-000 GUID 열에 많은 경우 있습니다 하지 않을 tooaggregate 해당 값입니다. 하기 전에 집계를 작성할 수 있습니다 "WHERE GUID!" 000 000 000 "=" toofilter hello 고주파 값입니다.

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a>옵션 2: 다른 파티션 또는 배포 키 선택

예제에서는 앞에 오는 hello만 toocheck hello 세금 감사 작업 하려는 경우 국가 hello를 통해 모든, hello ID 번호 키로 선택 하 여 hello 데이터 분산을 향상 시킬 수 있습니다. 다른 파티션 또는 배포 키를 선택 하는 경우에 따라 데이터를 배포할 수 hello 보다 균등 하 게 하지만이 옵션을이 선택 하지 않는 비즈니스 논리에 영향을 toomake 필요 합니다. 예를 들어, toocalculate hello 세금 sum toodesignate 각 상태에 대 한 경우가 _상태_ hello 파티션 키로 합니다. Tooexperience이이 문제를 계속 하는 경우 옵션 3을 사용해 보세요.

### <a name="option-3-add-more-partition-or-distribution-keys"></a>옵션 3: 더 많은 파티션 또는 배포 키 추가

_주_만 파티션 키로 사용하는 대신 두 개 이상의 키를 분할에 사용할 수 있습니다. 예를 들어, 추가 _우편 번호_ 추가 파티션으로 키 tooreduce 데이터 파티션 크기를 조정 하 고 hello 데이터를 보다 균등 하 게 배포 합니다.

### <a name="option-4-use-round-robin-distribution"></a>옵션 4: 라운드 로빈 배포 사용

파티션 및 배포에 대 한 적절 한 키를 찾을 수 없는 경우 toouse 라운드 로빈 배포를 시도할 수 있습니다. 라운드 로빈 배포는 모든 행을 동등하게 처리하고 임의로 해당 버킷에 넣습니다. hello 데이터 가져옵니다 균등 하 게, 그러나 집약성 정보, 일부 작업에 대 한 작업 성능이 저하 될 수 있는 단점이 있습니다. 또한 그래도 hello 왜곡 된 키에 대 한 집계를 수행 하는, hello 데이터 불일치가 문제가 지속 됩니다. 라운드 로빈 배포에 대해 자세히 toolearn hello U-SQL 테이블 분포 참조 섹션 [CREATE TABLE (SQL U): 스키마가 있는 테이블 만들기](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch)합니다.

## <a name="solution-2-improve-hello-query-plan"></a>해결 방법 2: hello 쿼리 계획을 향상 시킵니다.

### <a name="option-1-use-hello-create-statistics-statement"></a>옵션 1: hello CREATE STATISTICS 문을 사용 하 여

U-SQL 테이블 hello CREATE STATISTICS 문을 제공합니다. 이 문은 hello 데이터 등의 특성 값 분포 테이블에 저장 하는 방법에 대 한 자세한 내용은 toohello 쿼리 최적화를 제공 합니다. 대부분의 쿼리에서 hello 쿼리 최적화 프로그램에서 이미-고품질의 쿼리 계획에 대 한 hello 필요한 통계를 생성합니다. 경우에 따라서는 추가 통계 CREATE STATISTICS를 작성 하거나 hello 쿼리 디자인을 수정 하 여 tooimprove 쿼리 성능을 할 수 있습니다. 자세한 내용은 참조 hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) 페이지.

코드 예제:

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
>통계 정보는 자동으로 업데이트되지 않습니다. Hello 통계를 다시 만들지 않고 hello 테이블의에서 데이터를 업데이트 하는 경우 hello 쿼리 성능이 저하 될 수 있습니다.

### <a name="option-2-use-skewfactor"></a>옵션 2: SKEWFACTOR 사용

각 상태에 대 한 toosum hello 세금을 원하는 경우 상태 그룹별 hello 데이터 불일치가 문제를 방지 하지 않는 한 방법을 사용 해야 합니다. 그러나 데이터 왜곡 키 hello 최적화 프로그램을 실행 계획을 준비할 수 있도록 하 여 쿼리 tooidentify에 데이터 힌트를 제공할 수 있습니다.

일반적으로 0.5과 1 매우 기울이기 및 1 의미 중형 오차를 의미 하는 0.5로 hello 매개 변수를 설정할 수 있습니다. Hello 힌트 hello 현재 문과 모든 다운스트림에 대 한 실행 계획이 최적화에 영향을 주므로 되기까지 있는지 tooadd hello 힌트 hello 잠재적인 왜곡 key-wise 집계 합니다.

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

코드 예제:

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a>옵션 3: ROWCOUNT 사용  
또한 tooSKEWFACTOR 특정 비대칭 키에 대 한 연결의 경우, 해당 hello를 알고 있는 경우 다른 조인 된 행 집합 크기가 작은, 조인 하기 전에 hello U-SQL 문에서 행 개수 힌트를 추가 하 여 hello 최적화 프로그램을 확인할 수 있습니다. 이러한 방식으로 최적화 프로그램 브로드캐스트 조인 전략 toohelp 성능을 향상 시킬 선택할 수 있습니다. 행 개수 hello 데이터 불일치가 문제가 해결 되지 않으면 아니라 몇 가지 추가 도움말을 얻을 수 있는 됩니다.

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

코드 예제:

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a>해결 방법 3: hello 사용자 정의 리 듀 서 및 조합 기를 개선 합니다.

경우에 따라 복잡 한 프로세스 논리를 사용 하 여 사용자 정의 연산자 toodeal 쓰고 잘 작성 된 리 듀 서 및 조합 기 일부 경우에는 데이터 불일치가 문제를 완화 될 수 있습니다.

### <a name="option-1-use-a-recursive-reducer-if-possible"></a>옵션 1: 가능한 경우 재귀적(recursive) 리듀서 사용

기본적으로 사용자 정의 리듀서는 비재귀 모드로 실행됩니다. 즉, 키에 대한 작업을 줄이면 단일 꼭짓점으로 배포됩니다. 그러나 데이터가 비대칭 경우 hello 거 대 한 데이터 집합은 단일 꼭 짓 점 처리와 오랜 시간 동안 실행 될 수 있습니다.

tooimprove 성능 프로그램 코드 toodefine 리 듀 서 toorun 반복 모드에서에서 특성을 추가할 수 있습니다. 그런 다음 hello 거 대 한 데이터 집합 분산된 toomultiple 꼭 짓 점 수 있으며 작업 속도가 향상 병렬로 실행 됩니다.

비재귀적 리 듀 서 toorecursive toochange toomake 알고리즘 연관 되는지 확인 해야 합니다. 예를 들어 hello 합계가 결합 되며 hello 중간값 없습니다. 또한 toomake 입력 hello 및 리 듀 서에 대 한 출력 hello 유지 해야 동일한 스키마입니다.

재귀적 리듀서의 특성:

    [SqlUserDefinedReducer(IsRecursive = true)]

코드 예제:

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a>옵션 2: 가능한 경우 행 수준 결합자 모드 사용

특정 키가 일치 하지 않아 조인 사례에 대 한 유사한 toohello ROWCOUNT 힌트를 결합 모드 hello 작업을 동시에 실행할 수 있도록 toodistribute 큰 왜곡 키 값 집합 toomultiple 꼭지점을 시도 합니다. 결합자 모드는 데이터 기울이기 문제를 해결할 수는 없지만 기울어진 대량 키 값 집합에 추가적인 도움을 줄 수 있습니다.

기본적으로 hello 결합 모드 꽉 참, hello 행 집합을 왼쪽 및 오른쪽 행 집합을 분리할 수 없는 의미 합니다. 왼쪽/오른쪽/내부도 hello 모드 설정에는 행 수준 조인 수 있습니다. hello 시스템 hello 해당 행 집합을 나누고 병렬로 실행 되는 여러 꼭지점에 배포 합니다. 그러나 hello 결합 모드를 구성 하기 전에 해당 행 집합 hello tooensure를 분리할 때 주의 해야 합니다.

뒤에 오는 hello 예제는 분리 된 왼쪽된 행 집합을 보여 줍니다. 각 출력 행 hello 왼쪽에서 단일 입력된 행에 따라 다르며 잠재적으로 종속 hello hello 오른쪽으로에서 모든 행에 동일한 키 값입니다. 왼쪽으로 hello 결합 모드를 설정 하면 hello 시스템 hello 거 대 한 왼쪽-행 집합을 작은 것으로 나누고 toomultiple 꼭지점을 할당 합니다.

![결합자 모드 그림](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
>Hello 잘못 된 조합 기 모드를 설정 하면 hello 조합 조금 덜 효율적 이며 hello 결과가 잘못 될 수 있습니다.

결합자 모드의 특성:

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- SqlUserDefinedCombiner(Mode=CombinerMode.Left): 모든 출력 행 hello 왼쪽에서 단일 입력된 행에 따라 달라 집니다 (및 잠재적으로 모든 행 hello hello로 오른쪽에서 동일한 키 값).

- qlUserDefinedCombiner(Mode=CombinerMode.Right): hello 오른쪽에서 단일 입력된 행에 모든 출력 행에 따라 달라 집니다 (및 잠재적으로 모든 행 hello로 hello 왼쪽에서 동일한 키 값).

- SqlUserDefinedCombiner(Mode=CombinerMode.Inner): 모든 출력 행에 따라 달라 집니다 hello 왼쪽 및 오른쪽 hello hello에서 단일 입력된 행을 동일한 값입니다.

코드 예제:

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }

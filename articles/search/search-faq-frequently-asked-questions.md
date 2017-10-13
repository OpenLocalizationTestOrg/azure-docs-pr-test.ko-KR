---
title: "Azure Search에 대한 질문과 대답(FAQ) | Microsoft Docs"
description: "Microsoft Azure Search 서비스에 대한 일반적인 질문과 답변"
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 02d5fac8cf9067ec544668f306fe49b805b3d164
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Azure Search - FAQ(질문과 대답)
 
 Azure Search와 관련된 개념, 코드, 시나리오에 대한 일반적인 질문의 답변을 알아봅니다.

## <a name="platform"></a>플랫폼

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>Azure Search가 DBMS의 전체 텍스트 검색과 어떻게 다릅니까?

Azure Search에서는 여러 데이터 원본, [다국어 언어 분석](https://docs.microsoft.com/rest/api/searchservice/language-support), [흥미롭고 일반적이지 않은 데이터 입력에 대한 사용자 지정 분석](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search), [점수 매기기 프로필](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)을 통한 검색 순위 관리, 사용자 환경 특징(예: 미리 입력, 적중 항목 강조 표시, 패싯 탐색)을 지원합니다. 또한 동의어 및 다양한 쿼리 구문 등과 같은 다른 기능도 지원하지만 보통은 차별화된 기능이 아닙니다.

### <a name="what-is-the-difference-between-azure-search-and-elasticsearch"></a>Azure Search과 Elasticsearch의 차이는 무엇입니까?

검색 기술을 비교할 때 고객은 Azure Search와 Elasticsearch의 특정한 차이점에 대해 자주 질문합니다. 고객은 보통 Azure Search가 주요 업무를 더 쉽게 해 주거나 타 Microsoft 기술과의 기본 제공 통합이 필요하기 때문에 검색 응용 프로그램으로 Elasticsearch 대신 Azure Search를 선택합니다.

+ Azure Search는 충분한 중복 구성(읽기 액세스용 복제본 2개, 읽기-쓰기용 복제본 3개)을 통해 프로비전 시 99.9%의 서비스 수준 계약(SLA)을 제공하는 완전 관리형 클라우드 서비스입니다.
+ Microsoft의 [자연어 프로세서](https://docs.microsoft.com/rest/api/searchservice/language-support)는 첨단 언어 분석을 제공합니다.  
+ [Azure Search 인덱서](search-indexer-overview.md)는 초기 및 중분 인덱싱을 위해 다양한 Azure 데이터 소스를 탐색합니다.
+ 쿼리나 인덱싱 볼륨의 변동에 신속히 응대해야 할 경우 Azure Portal의 [슬라이더 컨트롤](search-manage.md#scale-up-or-down)을 사용하거나 [PowerShell 스크립트](search-manage-powershell.md)를 실행하여 직접 분할된 데이터베이스 관리를 무시합니다.  
+ [점수 매기기 및 조정 기능](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)은 검색 엔진이 단독으로 제공 가능하던 것을 넘어 검색 순위 점수에 영향을 미치는 방법을 제공합니다. 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>Azure Search를 일시 중지하고 청구를 멈출 수 있습니까?

서비스는 일시 중지할 수 없습니다. 서비스가 만들어지면 고객의 독점적 사용을 위해 계산 및 저장소 리소스가 할당됩니다. 요청에 따라 이러한 리소스를 해제하고 재청구하는 것은 불가능합니다. 

## <a name="indexing-operations"></a>인덱싱 작업

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>인덱스나 인덱스 스냅숏의 백업 및 복원(또는 다운로드 및 이동)

언제든 [인덱스 정의를 가져올 수](https://docs.microsoft.com/rest/api/searchservice/get-index) 있지만 클라우드 시스템에서 실행되는 *채워진* 인덱스를 로컬 시스템에 다운로드하거나 다른 Azure Search 서비스로 이동하기 위한 인덱스 추출, 스냅숏 또는 백업-복원 기능은 없습니다. 

인덱스는 사용자가 작성한 코드에서 구축 및 채워지며 클라우드에서는 오직 Azure Search 상에서 실행됩니다. 일반적으로 인덱스를 다른 서비스로 이동하려는 고객은 새 끝점을 사용하게 코드를 편집한 다음 인덱싱을 다시 실행하여 그렇게 하게 됩니다. 스냅숏 만들기나 인덱스 백업 기능이 필요한 경우 [사용자 의견](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index)을 남겨 주시기 바랍니다.

### <a name="can-i-index-from-sql-database-replicas-applies-to-azure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>SQL 데이터베이스 복제본에서 인덱싱할 수 있나요?([Azure SQL Database 인덱서](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers)에 적용)

 처음부터 새롭게 인덱스를 구축할 때 주 또는 보조 복제본을 데이터 원본으로 사용하는 데는 제약이 없습니다. 그러나 증분 업데이트(변경된 레코드 기준)를 통해 인덱스를 새로 고칠 때는 주 복제본이 필요합니다. 이것은 주 복제본에서만 변경 추적을 보장하는 SQL Database에 따른 요구 사항입니다. 인덱스 새로 고침 작업에 보조 복제본을 사용할 경우 전체 데이터를 확보한다고는 보장할 수 없습니다.

## <a name="search-operations"></a>검색 작업

### <a name="can-i-search-across-multiple-indexes"></a>여러 인덱스에서 검색할 수 있나요?

아니요. 이 작업은 지원되지 않습니다. 검색 범위는 항상 단일 인덱스입니다.

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>사용자 ID로 검색 모음 액세스를 제한할 수 있나요?

Azure Search에는 사용자별 데이터 액세스를 위한 역할 기반 보안 모델이 없습니다. 인증은 서비스 수준에서 전체 권한 또는 읽기 전용입니다. 일부 고객은 [ `$filter` 검색 매개 변수](https://docs.microsoft.com/rest/api/searchservice/search-documents)를 기반으로 솔루션을 구현하나 차선책에 불과합니다. 이 기능이 필요하면 [사용자 의견](https://feedback.azure.com/forums/263029-azure-search/category/86074-security)을 남겨 주세요.

### <a name="why-are-there-zero-matches-on-terms-i-know-to-be-valid"></a>유효하다고 알고 있는 용어에 대해 일치가 0인 이유는 무엇인가요?

가장 일반적인 경우는 각 쿼리 입력이 언어적 분석의 다른 검색 동작과 수준을 지원하는 것을 인지하지 못하기 때문입니다. 핵심 작업인 전체 텍스트 검색에는 용어를 근본 형태로 분석하는 언어 분석 단계가 포함됩니다. 토큰화된 용어는 더 많은 변형 항목과 일치하기 때문에 이 쿼리 구문 분석 단계에는 가능한 일치보다 범위가 더 넓어집니다.

[다른 쿼리 유형](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)(와일드 카드 검색, 유사 항목 검색, 근접 검색, 제안 등)을 호출할 경우 언어 분석이 없습니다. 용어가 있는 그대로 쿼리 트리에 추가됩니다. 

### <a name="why-is-the-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>검색 순위가 일정하거나 모든 적중에 대해 점수가 1.0으로 같은 이유는 무엇인가요?

기본적으로 검색 결과는 [일치하는 용어의 통계적 속성](search-lucene-query-architecture.md#stage-4-scoring)에 따라 점수가 매겨지며 결과 집합에서 높은 점수에서 낮은 점수 순으로 순위가 매겨집니다. 그러나 일부 쿼리 유형(와일드카드, 접두사, regex)은 전체적인 문서 점수에 항상 상수 점수를 부여합니다. 이 동작은 의도된 것입니다. Azure Search는 순위 영향 없이 쿼리 확장을 통해 검색된 일치 항목이 결과에는 포함되게 하기 위해 일정 점수를 적용합니다. 

예를 들어, 와일드카드 검색에서 "tour*"를 입력하면 "tours", "tourettes" 및 "tourmaline"이 일치합니다. 이러한 결과의 특성을 감안할 때, 어떤 용어가 더 중요한지 합리적으로 유추할 방법이 없습니다. 이러한 이유로 와일드카드, 접두사, regex 쿼리 유형의 결과에 대한 점수를 매길 때에는 용어 빈도를 무시합니다. 예기치 않은 일치의 가능성에 따른 왜곡을 방지하기 위해 부분 이력 기준 검색 결과에는 일정 점수가 부여됩니다.

## <a name="design-patterns"></a>디자인 패턴

### <a name="what-is-the-best-approach-for-implementing-localized-search"></a>특정 언어 검색을 구현하기 위한 가장 좋은 방법은 무엇인가요?

대부분의 고객은 동일한 인덱스에서 다양한 로캘(언어)을 지원하기 위해 컬렉션보다 전용 필드를 선택합니다. 로캘 특정 필드를 사용하면 적합한 분석기를 할당할 수 있습니다. 예를 들어, 프랑스어 문자열이 들어간 필드에는 Microsoft French Analyzer를 할당합니다. 그렇게 하면 필터링도 간소화됩니다. 쿼리가 Fr-Fr 페이지에서 시작되었음을 알고 있다면 검색 결과를 이 필드로 제한할 수 있습니다. 또는 [점수 매기기 프로필](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)을 만들어 해당 필드에 더 상대적인 가중치를 부여합니다.

## <a name="next-steps"></a>다음 단계

없는 기능 또는 특징에 대해 질문이 있으면 [사용자 의견 웹 사이트](https://feedback.azure.com/forums/263029-azure-search)에서 요청하세요.

## <a name="see-also"></a>참고 항목

 [StackOverflow: Azure Search](https://stackoverflow.com/questions/tagged/azure-search)   
 [Azure Search의 전체 텍스트 검색 작동 방식](search-lucene-query-architecture.md)  
 [Azure Search란?](search-what-is-azure-search.md)

 
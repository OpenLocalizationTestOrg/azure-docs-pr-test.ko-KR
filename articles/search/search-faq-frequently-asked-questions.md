---
title: "질문과 대답 (FAQ) Azure 검색에 대 한 aaaFrequently | Microsoft Docs"
description: "Microsoft Azure 검색 서비스에 대 한 toocommon 질문과 답변을 가져오려면"
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 2c573750600d80585b746bfce20d6c0f8df5a262
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Azure Search - FAQ(질문과 대답)
 
 대답 toocommonly에 대 한 질문과 개념, 코드 및 시나리오 관련 tooAzure 검색을 찾습니다.

## <a name="platform"></a>플랫폼

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>Azure Search가 DBMS의 전체 텍스트 검색과 어떻게 다릅니까?

Azure Search에서는 여러 데이터 원본, [다국어 언어 분석](https://docs.microsoft.com/rest/api/searchservice/language-support), [흥미롭고 일반적이지 않은 데이터 입력에 대한 사용자 지정 분석](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search), [점수 매기기 프로필](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)을 통한 검색 순위 관리, 사용자 환경 특징(예: 미리 입력, 적중 항목 강조 표시, 패싯 탐색)을 지원합니다. 또한 동의어 및 다양한 쿼리 구문 등과 같은 다른 기능도 지원하지만 보통은 차별화된 기능이 아닙니다.

### <a name="what-is-hello-difference-between-azure-search-and-elasticsearch"></a>Azure 검색와 Elasticsearch hello 차이 무엇입니까?

검색 기술을 비교할 때 고객은 Azure Search와 Elasticsearch의 특정한 차이점에 대해 자주 질문합니다. 선택한 경우 Azure 검색 Elasticsearch를 통해 해당 검색에 대 한 응용 프로그램 프로젝트 일반적으로 주요 태스크를 보다 쉽게 바뀌었고 또는 hello와 다른 Microsoft 기술의 기본 제공 통합 필요 하기 때문에 수행 합니다.

+ Azure Search는 충분한 중복 구성(읽기 액세스용 복제본 2개, 읽기-쓰기용 복제본 3개)을 통해 프로비전 시 99.9%의 서비스 수준 계약(SLA)을 제공하는 완전 관리형 클라우드 서비스입니다.
+ Microsoft의 [자연어 프로세서](https://docs.microsoft.com/rest/api/searchservice/language-support)는 첨단 언어 분석을 제공합니다.  
+ [Azure Search 인덱서](search-indexer-overview.md)는 초기 및 중분 인덱싱을 위해 다양한 Azure 데이터 소스를 탐색합니다.
+ 쿼리 또는 인덱싱 볼륨에서 toofluctuations 신속 하 게 응답 해야 하는 경우 사용할 수 있습니다 [슬라이더 컨트롤](search-manage.md#scale-up-or-down) hello Azure 포털에서 또는 실행에 [PowerShell 스크립트](search-manage-powershell.md)를 직접 분할 관리를 무시 합니다.  
+ [점수 매기기 및 조정 기능](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) hello 검색 순위 점수가 어떤 hello 검색 엔진만 제공할 수 초과 영향을 주는 대 한 의미를 제공 합니다. 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>Azure Search를 일시 중지하고 청구를 멈출 수 있습니까?

Hello 서비스를 일시 중지할 수 없습니다. Hello 서비스를 만드는 경우 배타적 사용에 대 한 계산 및 저장소 리소스가 할당 됩니다. 가능한 toorelease 아니며 해당 요청 시 리소스를 회수 합니다. 

## <a name="indexing-operations"></a>인덱싱 작업

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>인덱스나 인덱스 스냅숏의 백업 및 복원(또는 다운로드 및 이동)

수 있지만 [인덱스 정의 가져올](https://docs.microsoft.com/rest/api/searchservice/get-index) 언제 든 지 인덱스 추출, 스냅숏, 또는 없을 백업 복원 기능을 다운로드 하기 위한는 *채워진* hello 클라우드 tooa 로컬 시스템에서 실행 하는 인덱스 또는 Azure 검색 서비스 tooanother 이동 합니다. 

인덱스는 작성, 쓰기 및 hello 클라우드에서 Azure 검색에 대해서만 실행 하는 코드에서 채워집니다. 일반적으로 toomove 인덱스 tooanother 서비스 사용자가 자신의 코드 toouse 새 끝점을 편집 하 여 하 고 인덱스를 다시 실행 하십시오. Hello 기능 tootake 스냅숏으로 하거나 인덱스를 백업, 경우 투표 캐스팅 [사용자 음성](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index)합니다.

### <a name="can-i-index-from-sql-database-replicas-applies-tooazure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>SQL 데이터베이스 복제본에서 있습니까 인덱싱할 수 (너무 적용[Azure SQL 데이터베이스 인덱서](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers))

 제한 사항이 없습니다 hello 사용 시 기본 또는 보조 복제본의 데이터 원본으로 처음부터 인덱스를 작성 하는 경우입니다. 그러나 증분 업데이트 (변경 된 레코드에 기반)와 인덱스를 새로 고치면 hello 주 복제본이 필요 합니다. 이것은 주 복제본에서만 변경 추적을 보장하는 SQL Database에 따른 요구 사항입니다. 보조 복제본을 사용 하 여 인덱스 새로 고침 작업을 시도 하면에 hello 데이터는 모든 아닙니다.

## <a name="search-operations"></a>검색 작업

### <a name="can-i-search-across-multiple-indexes"></a>여러 인덱스에서 검색할 수 있나요?

아니요. 이 작업은 지원되지 않습니다. 검색은 항상 tooa 범위가 지정 된 단일 인덱스입니다.

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>사용자 ID로 검색 모음 액세스를 제한할 수 있나요?

Azure Search에는 사용자별 데이터 액세스를 위한 역할 기반 보안 모델이 없습니다. 인증은 전체 권한 중 하나 또는 hello 서비스 수준에서 읽기 전용입니다. 일부 고객은 [ `$filter` 검색 매개 변수](https://docs.microsoft.com/rest/api/searchservice/search-documents)를 기반으로 솔루션을 구현하나 차선책에 불과합니다. 이 기능이 필요하면 [사용자 의견](https://feedback.azure.com/forums/263029-azure-search/category/86074-security)을 남겨 주세요.

### <a name="why-are-there-zero-matches-on-terms-i-know-toobe-valid"></a>유효한 toobe 여부를 확인 하는 용어에 대해 일치 0 이유는 무엇입니까?

hello 가장 일반적인 경우 다른 검색 동작 및 언어적 분석 수준의 각 쿼리 유형을 지원 하는지 알아야 되지 않습니다. Hello 주된 작업 인 전체 텍스트 검색 tooroot forms 아래로 용어를 중단 하는 언어 분석 단계를 포함 합니다. 쿼리 구문 분석에서이 측면이 일치 하기 때문에 hello 토큰화 된 용어는 더 많은 수의 변형 가능한 일치 항목을 통해 보다 광범위 한 net을 캐스팅 합니다.

[다른 쿼리 유형](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)(와일드 카드 검색, 유사 항목 검색, 근접 검색, 제안 등)을 호출할 경우 언어 분석이 없습니다. 용어 toohello 쿼리 트리에 추가 된-됩니다. 

### <a name="why-is-hello-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>이유 hello 검색 순위를 1.0 공격에 대 한 상수와 같거나 점수는 무엇입니까?

기본적으로 검색 결과 따라 점수가 따라 hello에 [용어 일치의 통계 속성과](search-lucene-query-architecture.md#stage-4-scoring), 높은 toolow hello 결과 집합에 정렬 합니다. 그러나 몇 가지 쿼리 유형 (와일드 카드, 접두사, regex) 항상 상수 점수가 기여 toohello 전체 점수를 문서화 합니다. 이 동작은 의도된 것입니다. Azure 검색 사항이 상수 hello 순위에 영향을 주지 않고 hello 결과에 포함 된 쿼리 확장 toobe 통해 찾은 tooallow 일치 점수를 매깁니다. 

예를 들어, 와일드카드 검색에서 "tour*"를 입력하면 "tours", "tourettes" 및 "tourmaline"이 일치합니다. 이러한 결과의 hello 특성 들어 방법이 없습니다 tooreasonably 유추는 용어는 다른 항목 보다 더 중요 합니다. 이러한 이유로 와일드카드, 접두사, regex 쿼리 유형의 결과에 대한 점수를 매길 때에는 용어 빈도를 무시합니다. 일부 입력에 따라 검색 결과 상수를 제공 됩니다 tooavoid 바이어스 예기치 않은 잠재적으로 일치 항목으로 점수를 매깁니다.

## <a name="design-patterns"></a>디자인 패턴

### <a name="what-is-hello-best-approach-for-implementing-localized-search"></a>지역화 된 검색을 구현 하기 위한 hello 가장 좋은 방법은 무엇입니까?

Toosupporting 다른 로캘을 (언어) hello에 있어 컬렉션 전용된 필드는 대부분의 고객 선택 같은 인덱스입니다. 로캘 관련 필드 가능한 tooassign을 적절 한 분석기 만듭니다. 예를 들어 프랑스어 문자열을 포함 하는 hello Microsoft 프랑스어 분석기 tooa 필드를 할당 하려고 했습니다. 그렇게 하면 필터링도 간소화됩니다. Fr-fr 페이지에서 시작 되는 쿼리를 알고 있는 경우 검색 결과 toothis 필드를 제한 될 수 있습니다. 또는 만들는 [점수 매기기 프로필](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) toogive hello 필드 상대 가중치를 더 부여 합니다.

## <a name="next-steps"></a>다음 단계

없는 기능 또는 특징에 대해 질문이 있으면 Hello에 hello 기능 요청 [사용자 의견 웹 사이트](https://feedback.azure.com/forums/263029-azure-search)합니다.

## <a name="see-also"></a>참고 항목

 [StackOverflow: Azure Search](https://stackoverflow.com/questions/tagged/azure-search)   
 [Azure Search의 전체 텍스트 검색 작동 방식](search-lucene-query-architecture.md)  
 [Azure Search란?](search-what-is-azure-search.md)

 
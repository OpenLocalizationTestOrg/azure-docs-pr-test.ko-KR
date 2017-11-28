# 개요
## [Azure 검색이란?](search-what-is-azure-search.md)
# 시작
## [SKU 선택](search-sku-tier.md)
## [서비스 만들기](search-create-service-portal.md)
## [인덱스 만들기](search-what-is-an-index.md)
### [Azure Portal](search-create-index-portal.md)
### [.NET](search-create-index-dotnet.md)
### [REST](search-create-index-rest-api.md)
## [데이터 추가](search-what-is-data-import.md)
### [Azure Portal](search-import-data-portal.md)
### [.NET](search-import-data-dotnet.md)
### [REST](search-import-data-rest-api.md)
## [인덱스 검색](search-query-overview.md)
### [Azure Portal](search-explorer.md)
### [.NET](search-query-dotnet.md)
### [REST (영문)](search-query-rest-api.md)
# 자습서
## [.NET](search-howto-dotnet-sdk.md)
## [.NET 동의어 미리 보기](search-synonyms-tutorial-sdk.md)
## [포털](search-get-started-portal.md)
## [Node.JS](search-get-started-nodejs.md)
## [Java](search-get-started-java.md)
# 방법
## 계획 및 디자인
### [서비스 한도](search-limits-quotas-capacity.md)
### [서비스 확장성](search-capacity-planning.md)
### [다중 테넌트 지원을 위한 디자인 패턴](search-modeling-multitenant-saas-applications.md)

## 개발
### [API 버전](search-api-versions.md)
### [Hello SDK를 업그레이드 합니다.](search-dotnet-sdk-migration.md)
### [업그레이드 hello REST API](search-api-migration.md)
### [복합 데이터 형식 모델링](search-howto-complex-data-types.md)
### [동시 업데이트 처리](search-howto-concurrency.md)
### [코드 샘플](https://azure.microsoft.com/resources/samples/?service=search)

## 관리
### Azure Search 관리
#### [Azure 포털](search-manage.md)
#### [PowerShell](search-manage-powershell.md)
### [사용 및 통계 모니터링](search-monitor-usage.md)
### [트래픽 분석 검색](search-traffic-analytics.md)
### [성능 및 최적화](search-performance-optimization.md)
## 데이터 로드
### [인덱서 개요](search-indexer-overview.md)
### [Azure Blob Storage 인덱서](search-howto-indexing-azure-blob-storage.md)
### [Azure Table Storage 인덱서](search-howto-indexing-azure-tables.md)
### [Azure SQL 인덱서](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
### [Azure Cosmos DB 인덱서](search-howto-index-documentdb.md)
### [인덱스 CSV blob](search-howto-index-csv-blobs.md)
### [인덱스 JSON blob](search-howto-index-json-blobs.md)
### [Azure VM에서 인덱서 연결 tooSQL 서버 구성](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md)
### [인덱서의 필드 매핑](search-indexer-field-mappings.md)
##  Search
### [전체 텍스트 검색 작동 방식](search-lucene-query-architecture.md)
### 쿼리 생성
#### [단순 쿼리 구문](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)
#### [Lucene 쿼리 구문](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)
#### [Lucene 구문 쿼리 예제](search-query-lucene-examples.md)
#### [필터 식 구문](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)
### 사용자 지정 검색
#### [언어 분석기](https://docs.microsoft.com/rest/api/searchservice/language-support)
#### [사용자 지정 분석기](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search)
### [페이징 결과](search-pagination-page-layout.md)
### [점수 매기기](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)
### [제안](https://docs.microsoft.com/rest/api/searchservice/suggesters)
### [패싯 탐색](search-faceted-navigation.md)
### [동의어 미리 보기](search-synonyms.md)

# 참조

## [.NET](/dotnet/api/?term=microsoft.azure.search)
## [.NET(관리)](/dotnet/api/?term=microsoft.azure.management.search)
## [Python(관리)](http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.mgmt.search.html)
## [REST (영문)](/rest/api/searchservice)
## [REST(관리)](/rest/api/searchmanagement)
## [서비스 REST(미리 보기)](search-api-2015-02-28-preview.md)

# 리소스

## [Azure 로드맵](https://azure.microsoft.com/roadmap/?category=web-mobile)
## [질문과 대답(FAQ)](search-faq-frequently-asked-questions.md)
## [가격](https://azure.microsoft.com/pricing/details/search/)
## [요금 계산기](https://azure.microsoft.com/pricing/calculator/)
## [서비스 업데이트](https://azure.microsoft.com/updates/?product=search)
## 코스웨어 및 자습서
### [비디오 및 자습서](search-video-demo-tutorial-list.md)
### [Virtual Academy](https://mva.microsoft.com/training-courses/using-windows-azure-search-10540?l=ADkxnd97_9304984382)
## 데모 사이트
### [검색 분석기 데모](http://alice.unearth.ai/)
### [라이브 데모 앱](https://searchsamples.azurewebsites.net/)
### [작업 목록 앱](http://aka.ms/azjobsdemo)
## 파트너 및 커뮤니티
### [Azure Search GitHub](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search)
### [MSDN 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureSearch)
### [스택 오버플로](http://stackoverflow.com/questions/tagged/azure-search)
### [블로그: 관계형 데이터 모델링](http://blogs.technet.com/b/onsearch/archive/2015/09/08/modeling-the-adventureworks-inventory-database-for-azure-search.aspx)
### [[블로그: 다단계 패싱](http://blogs.technet.com/b/onsearch/archive/2015/09/09/multi-level-taxonomy-facets-in-azure-search.aspx)




---
title: "aaaAzure Cosmos DB.NET SDK 및 리소스 | Microsoft Docs"
description: ".NET API 및 SDK 릴리스 날짜, 사용 중지 날짜 및 hello Cosmos DB AZURE.NET SDK의 각 버전 간의 변경 내용을 포함 하 여 hello에 대 한 모든에 대해 알아봅니다."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a>Azure Cosmos DB .NET SDK: 다운로드 및 릴리스 정보
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [.NET 변경 피드](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.JS](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST (영문)](https://docs.microsoft.com/rest/api/documentdb/)
> * [REST 리소스 공급자](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**SDK 다운로드**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td>**API 설명서**</td><td>[.NET API 참조 설명서](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**샘플**</td><td>[.NET 코드 샘플](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**시작**</td><td>[Cosmos DB AZURE.NET SDK hello로 시작.](documentdb-get-started.md)</td></tr>

<tr><td>**웹앱 자습서**</td><td>[Azure Cosmos DB를 사용한 웹 응용 프로그램 개발](documentdb-dotnet-application.md)</td></tr>

<tr><td>**현재 지원되는 프레임워크**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>릴리스 정보

### <a name="a-name11701170"></a><a name="1.17.0"/>1.17.0 

* 쿼리 결과 tooa 특정 파티션 키 범위 값의 범위를 지정 하는 것에 대 한 FeedOption으로 PartitionKeyRangeId에 대 한 지원이 추가 되었습니다. 
* 해당 시간 이후에 hello 변경 내용 검색 ChangeFeedOption toostart로 StartTime에 대 한 지원이 추가 되었습니다.

### <a name="a-name11611161"></a><a name="1.16.1"/>1.16.1
* Hello 스택 오버플로 예외를 일으킬 수 있는 JsonSerializable 클래스에에서는 문제가 해결 되었습니다.

### <a name="a-name11601160"></a><a name="1.16.0"/>1.16.0
*   Hello DocumentClient 생성자에서 선택적 매개 변수로 인해 JsonSerializerSettings toohello 도입 hello 응용 프로그램의 다시 컴파일하는 데 필요한 문제를 해결 합니다.
* 표시 된 hello DocumentClient 사용 되지 않는 생성자에 JsonSerializerSettings 매개 변수를 전달할 때 ConnectionPolicy 및 ConsistencyLevel 매개 변수 기본값에 대 한 마지막 매개 변수 tooallow hello와 JsonSerializerSettings를 필요한입니다.

### <a name="a-name11501150"></a><a name="1.15.0"/>1.15.0
*   [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet)를 인스턴스화하는 동안 사용자 지정 JsonSerializerSettings를 지정하기 위한 지원을 추가하였습니다.

### <a name="a-name11411141"></a><a name="1.14.1"/>1.14.1
*   SSE4 명령을 지원하지 않고 Azure Cosmos DB DocumentDB API 쿼리를 실행할 때 SEHException을 throw하는 x64 컴퓨터에 영향을 준 문제가 해결되었습니다.

### <a name="a-name11401140"></a><a name="1.14.0"/>1.14.0
*   ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.
*   개별 파티션의 쿼리 메트릭에 대한 지원이 추가되었습니다.
*   쿼리에 대 한 hello 연속 토큰의 hello 크기 제한에 대 한 지원이 추가 되었습니다.
*   실패한 요청의 자세한 추적에 대한 지원이 추가되었습니다.
*   Hello SDK 일부 성능 향상이 되었습니다.

### <a name="a-name11341134"></a><a name="1.13.4"/>1.13.4
* 기능적으로 1.13.3과 동일합니다. 내부적으로 약간 변경되었습니다.

### <a name="a-name11331133"></a><a name="1.13.3"/>1.13.3
* 기능적으로 1.13.2와 동일합니다. 내부적으로 약간 변경되었습니다.

### <a name="a-name11321132"></a><a name="1.13.2"/>1.13.2
* 집계 쿼리에 대 한 FeedOptions에 제공 된 hello PartitionKey 값을 무시 하는 문제가 해결 되었습니다.
* 플라이트 중간의 파티션 간 Order By 쿼리를 실행하는 동안 파티션 관리의 투명한 처리 문제를 해결했습니다.

### <a name="a-name11311131"></a><a name="1.13.1"/>1.13.1
* Hello 비동기 ASP.NET 컨텍스트 내에서 사용 하는 경우 Api의 일부에서 교착 상태를 일으킨 문제가 해결 되었습니다.

### <a name="a-name11301130"></a><a name="1.13.0"/>1.13.0
* SDK toomake 더 해결 특정 조건에서 탄력적인 tooautomatic 장애 조치 합니다.

### <a name="a-name11221122"></a><a name="1.12.2"/>1.12.2
* 경우에 따라 WebException을 야기 하는 문제에 대 한 수정: hello 원격 이름을 확인할 수 없습니다.
* 추가 된 hello 직접 새 오버 로드 tooReadDocumentAsync API를 추가 하 여 형식화 된 문서를 읽기 위한 지원 합니다.

### <a name="a-name11211121"></a><a name="1.12.1"/>1.12.1
* 집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 LINQ 지원이 추가되었습니다.
* 용 hello 이벤트 처리기를 사용 하 여 발생 하는 hello ConnectionPolicy 개체에 대 한 메모리 누수 문제를 수정 합니다.
* ETag를 사용할 때 UpsertAttachmentAsync가 작동하지 않는 문제를 해결합니다.
* 문자열 필드를 정렬할 때 파티션 간 order-by 쿼리 연속 작업이 작동하지 않는 문제를 해결합니다.

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* 집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다. [집계 지원](documentdb-sql-query.md#Aggregates)을 참조하세요.
* 10,100 000RU/s too2500 000RU/s에서 분할 된 컬렉션에 대해 최소 처리량을 적어집니다.

### <a name="a-name11141114"></a><a name="1.11.4"/>1.11.4
* 여기서 hello 32 비트 호스트 프로세스에 실패 했던 hello 크로스 파티션 쿼리의 일부 문제를 수정 하세요.
* 여기서 hello 세션 컨테이너 되 고 새로 고쳐지지 않았습니다 게이트웨이 모드에서 실패 한 요청에 대 한 hello 토큰으로 문제를 수정 하세요.
* 경우에 따라 프로젝션에서 UDF 호출을 사용하는 쿼리가 실패하는 문제를 수정했습니다.
* Hello 증가 하는 것에 대 한 클라이언트 쪽 성능 수정 읽고의 hello 요청 처리량을 작성 합니다.

### <a name="a-name11131113"></a><a name="1.11.3"/>1.11.3
* 여기서 hello 세션 컨테이너 업데이트 되지 않았습니다 되 고 실패 한 요청에 대 한 hello 토큰으로 문제를 수정 하세요.
* Hello SDK toowork 32 비트 호스트 프로세스에서에 대 한 지원이 추가 되었습니다. 파티션 간 쿼리를 사용하는 경우 향상된 성능을 위해 64비트 호스트를 처리하는 것이 좋습니다.
* IN 식에 많은 수의 파티션 키 값을 사용하는 쿼리와 관련된 시나리오의 성능이 향상되었습니다.
* PopulateQuotaInfo 요청 옵션이 설정 된 경우 문서 컬렉션 읽기 요청에 대 한 다양 한 리소스 할당량 stats를 ResourceResponse hello에 채워집니다.

### <a name="a-name11111111"></a><a name="1.11.1"/>1.11.1
* Hello 1.11.0에 도입 된 CreateDocumentCollectionIfNotExistsAsync API에 대 한 보조 성능 수정 합니다.
* 높은 수준의 동시 요청 수를 포함 하는 시나리오에 대 한 hello SDK의에서 성능 수정 합니다.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* 새 클래스 및 메서드 tooprocess hello에 대 한 지원 [피드 변경](change-feed.md) 컬렉션 내에서 문서입니다.
* 파티션 간 쿼리 연속 및 파티션 간 쿼리에 대한 일부 성능 향상 지원
* CreateDatabaseIfNotExistsAsync 및 CreateDocumentCollectionIfNotExistsAsync 메서드 추가
* 시스템 함수에 대한 LINQ 지원: IsDefined, IsNull 및 IsPrimitive
* 프로젝트에 project.json 도구와 hello Nuget 패키지를 사용 하는 경우 자동 binplacing Microsoft.Azure.Documents.ServiceInterop.dll 및 DocumentDB.Spatial.Sql.dll 어셈블리 tooapplication의 bin 폴더에 대 한 수정 합니다.
* 시나리오를 디버깅하는 데 도움이 될 수 있는 클라이언트 쪽 ETW 추적 내보내기 지원

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* 분할된 컬렉션에 대한 직접 연결 지원이 추가되었습니다.
* Hello Bounded Staleness 일관성 수준에 대 한 성능이 향상 됩니다.
* 지역 펜싱 공간 쿼리에 대한 컬렉션 인덱싱 정책을 지정하는 동안 Polygon 및 LineString 데이터 형식이 추가되었습니다.
* 조건자를 변환하는 동안 StringEnumConverter, IsoDateTimeConverter 및 UnixDateTimeConverter에 대한 LINQ 지원이 추가되었습니다.
* 다양한 SDK 버그가 수정되었습니다.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* 해당 않아 hello NotFoundException 다음 문제 해결: hello 세션 hello 입력된 세션 토큰을 사용할 수 없으면 읽기입니다. Hello 읽기 액세스 지리적으로 분산 계정의 지역에 대 한 쿼리 하는 경우에 따라이 예외가 발생 했습니다.
* Hello ResourceResponse 클래스를 통해 응답에서 toohello 내부 스트림에 대 한 직접 액세스의에서 hello ResponseStream 속성을 노출 합니다.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* 수정 된 hello ResourceResponse, FeedResponse, StoredProcedureResponse 및 MediaResponse 클래스 tooimplement hello (TDD) 배포를 제어 하는 테스트에 대 한 모의 수 있도록 공용 인터페이스에 해당 합니다.
* 데이터 직렬화를 위해 사용자 지정 JsonSerializerSettings 개체를 사용할 때 잘못된 파티션 키 헤더가 발생하는 문제가 수정되었습니다.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* 장기 실행 쿼리 toofail 오류로 인해 발생 하는 문제 해결: 권한 부여 토큰이 잘못 되었습니다. hello에 현재 시간입니다.
* 제거 하는 문제가 hello 크로스 파티션 top/order by 쿼리에서 원래 SqlParameterCollection 고정 합니다.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* 분할된 컬렉션에 대한 병렬 쿼리에 지원을 추가했습니다.
* 분할된 컬렉션에 대한 파티션 간 Order By 및 TOP 쿼리에 대한 지원을 추가했습니다.
* 누락 된 참조 tooDocumentDB.Spatial.Sql.dll 및 Microsoft.Azure.Documents.ServiceInterop.dll 참조 toohello Azure Cosmos DB Nuget 패키지와 프로그램 Cosmos DB Azure 프로젝트를 참조 하는 경우 필요 없는 고정된 번호입니다.
* LINQ에서 사용자 정의 함수를 사용할 때는 hello 기능 여러 유형의 toouse 매개 변수를 수정 했습니다. 
* Upsert 호출 쓰기 위치 대신 tooread 방향이 지정 된 위치를 되기 때문에 전역적으로 복제 된 계정에 대 한 버그를 수정 했습니다.
* 누락 된 추가 된 메서드 toohello IDocumentClient 인터페이스: 
  * mediaStream 및 options를 매개 변수로 사용하는 UpsertAttachmentAsync 메서드
  * options를 매개 변수로 사용하는 CreateAttachmentAsync 메서드
  * querySpec을 매개 변수로 사용하는 CreateOfferQuery 메서드
* Hello IDocumentClient 인터페이스에 노출 되는 봉인 되지 않은 공용 클래스입니다.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* 다중 영역 데이터베이스 계정에 대 한 추가 된 hello 지원 합니다.
* 정제된 요청에 대한 재시도 지원이 추가되었습니다.  사용자 hello 재시도 횟수를 사용자 지정할 수 및 hello ConnectionPolicy.RetryOptions 속성을 구성 하 여 hello 최대 대기 시간입니다.
* 모든 DocumenClient 속성 및 메서드의 hello 시그니처를 정의 하는 새 IDocumentClient 인터페이스를 추가 합니다.  이러한 변경의 일환으로, 또한 읽기 전용 이므로 hello DocumentClient 클래스 자체에서 IQueryable 및 IOrderedQueryable toomethods 만드는 확장 메서드
* 지정된 된 Azure Cosmos DB 끝점 Uri에 대 한 구성 옵션 tooset hello ServicePoint.ConnectionLimit 추가 됩니다.  Too50 설정 되어 있는 ConnectionPolicy.MaxConnectionLimit toochange hello 기본 값을 사용 합니다.
* IPartitionResolver와 해당 구현의 사용이 중단되었습니다.  IPartitionResolver 지원이 중단되었습니다. 보다 큰 저장소 및 처리량에는 파티션된 컬렉션을 사용하는 것이 좋습니다.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* 오버 로드 tooUri 기반 RequestOptions 매개 변수로 받아들이는 ExecuteStoredProcedureAsync 방법을 추가 했습니다.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* 문서에 대 한 시간 toolive (TTL) 지원이 추가 되었습니다.

### <a name="a-name163163"></a><a name="1.6.3"/>1.6.3
* Azure 클라우드 서비스 솔루션의 일부로 패키징에 대한 .NET SDK의 Nuget 패키징에서 버그가 수정되었습니다.

### <a name="a-name162162"></a><a name="1.6.2"/>1.6.2
* [분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다. 

### <a name="a-name153153"></a><a name="1.5.3"/>1.5.3
* **[고정]**  Azure Cosmos DB 쿼리 끝점 throw: ' System.Net.Http.HttpRequestException: 콘텐츠 tooa 스트림을 복사 하는 동안 오류 '.

### <a name="a-name152152"></a><a name="1.5.2"/>1.5.2
* 페이징, 조건식 및 범위 비교에 대한 새 연산자를 포함하는 LINQ 지원이 확장되었습니다.
  * Linq에서 연산자 tooenable SELECT TOP 동작 수행
  * CompareTo 연산자 tooenable 문자열 범위 비교
  * 조건부 (?) 및 병합 연산자 (??)
* **[수정됨]** 모델 프로젝션을 LINQ 쿼리의 Where-In과 결합할 때의 ArgumentOutOfRangeException이 수정되었습니다. [#81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* **[고정]**  선택 hello 마지막 식 hello 없으면 LINQ 공급자 프로젝션이 없습니다 것으로 간주 하 고 선택 생성 * 잘못 합니다.  [#58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Upsert가 구현되고 UpsertXXXAsync 메서드가 추가됨
* 모든 요청에 대한 성능 향상
* 문자열의 조건부, 병합 및 CompareTo 메서드에 대한 LINQ 공급자 지원
* **[고정]**  LINQ 공급자 구현 포함 목록 toogenerate에서 메서드 a b l e 및 배열에서와 동일한 SQL hello-->
* **[고정]**  BackoffRetryUtility 사용 하 여 다시 시도 새로 만드는 대신 다시 동일한 HttpRequestMessage hello
* **[사용되지 않음]** UriFactory.CreateCollection --> 이제 UriFactory.CreateDocumentCollection을 사용해야 합니다.

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1
* **[수정됨]** nl-NL 등과 같은 en 이외의 문화권 정보를 사용할 때의 지역화 문제 

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* ID 기반 라우팅 추가
  * ID 기반 리소스 링크를 작성 하는 새 UriFactory 도우미 tooassist
  * URI에 DocumentClient tootake에 새 오버 로드
* LINQ에서 지리 공간에 대한 IsValid() 및 IsValidDetailed() 추가됨
* LINQ 공급자 지원이 향상되었습니다.
  * **수학** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate
  * **문자열** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper
  * **배열** - Concat, Contains, Count
  * **IN** 연산자

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* 인덱싱 정책 수정 지원이 추가되었습니다.
  * DocumentClient의 새로운 ReplaceDocumentCollectionAsync 메서드
  * 인덱스 정책 변경 진행률을 추적하기 위한 ResourceResponse<T>의 새로운 IndexTransformationProgress 속성
  * 이제 DocumentCollection.IndexingPolicy를 변경할 수 있음
* 공간 인덱싱 및 쿼리 지원이 추가되었습니다.
  * 점 및 다각형과 같은 공간 형식을 직렬화/역직렬화하기 위한 새로운 Microsoft.Azure.Documents.Spatial 네임스페이스
  * Cosmos DB에 저장된 GeoJSON 데이터를 인덱싱하기 위한 새로운 SpatialIndex 클래스
* **[수정됨]** LINQ 식 [#38](https://github.com/Azure/azure-documentdb-net/issues/38)에서 생성된 잘못된 SQL 쿼리.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Newtonsoft.Json v5.0.7에 대한 종속성이 추가되었습니다.
* Order By toosupport 변경 했습니다.
  
  * OrderBy() 또는 OrderByDescending()에 대한 LINQ 공급자 지원
  * Order By IndexingPolicy toosupport 
    
    **가능한 주요 변경 내용** 
    
    사용자 지정 인덱싱 정책 사용 하 여 해당 프로 비전 컬렉션 기존 코드가 있는 경우 기존 프로그램 코드 요구 toobe toosupport hello 새 IndexingPolicy 클래스 업데이트. 사용자 지정 인덱싱 정책이 없다면 이 변경 사항은 영향을 주지 않습니다.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Hello 새 HashPartitionResolver 및 RangePartitionResolver 클래스와 IPartitionResolver hello를 사용 하 여 데이터를 분할 하는 것에 대 한 지원이 추가 되었습니다.
* DataContract serialization이 추가되었습니다.
* LINQ 공급자의 GUID 지원이 추가되었습니다.
* LINQ의 UDF 지원이 추가되었습니다.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK

## <a name="release--retirement-dates"></a>릴리스 및 사용 중지 날짜
Microsoft는 알림 최소 **12 개월** 순서 toosmooth hello 전환 tooa 지원/최신 버전의 SDK를 사용 중지 전에 합니다.

새로운 기능 및 기능 및 최적화는 toohello 현재만 추가 SDK, 따라서 것이 좋습니다 하면 항상 업그레이드 toohello 최신 SDK 버전 가능한 한 빨리 합니다. 

모든 요청 tooAzure 사용 중지 된 SDK를 사용 하 여 Cosmos DB hello 서비스에서 거부 됩니다.

<br/>

| 버전 | 릴리스 날짜 | 사용 중지 날짜 |
| --- | --- | --- |
| [1.17.0](#1.17.0) |2017년 8월 10일 |--- |
| [1.16.1](#1.16.1) |2017년 8월 7일 |--- |
| [1.16.0](#1.16.0) |2017년 8월 2일 |--- |
| [1.15.0](#1.15.0) |2017년 6월 30일 |--- |
| [1.14.1](#1.14.1) |2017년 5월 23일 |--- |
| [1.14.0](#1.14.0) |2017년 5월 10일 |--- |
| [1.13.4](#1.13.4) |2017년 5월 09일 |--- |
| [1.13.3](#1.13.3) |2017년 5월 06일 |--- |
| [1.13.2](#1.13.2) |2017년 4월 19일 |--- |
| [1.13.1](#1.13.1) |2017년 3월 29일 |--- |
| [1.13.0](#1.13.0) |2017년 3월 24일 |--- |
| [1.12.2](#1.12.2) |2017년 3월 20일 |--- |
| [1.12.1](#1.12.1) |2017년 3월 14일 |--- |
| [1.12.0](#1.12.0) |2017년 2월 15일 |--- |
| [1.11.4](#1.11.4) |2017년 2월 6일 |--- |
| [1.11.3](#1.11.3) |2017년 1월 26일 |--- |
| [1.11.1](#1.11.1) |2016년 12월 21일 |--- |
| [1.11.0](#1.11.0) |2016년 12월 8일 |--- |
| [1.10.0](#1.10.0) |2016년 9월 27일 |--- |
| [1.9.5](#1.9.5) |2016년 9월 1일 |--- |
| [1.9.4](#1.9.4) |2016년 8월 24일 |--- |
| [1.9.3](#1.9.3) |2016년 8월 15일 |--- |
| [1.9.2](#1.9.2) |2016년 7월 23일 |--- |
| [1.8.0](#1.8.0) |2016년 6월 14일 |--- |
| [1.7.1](#1.7.1) |2016년 5월 6일 |--- |
| [1.7.0](#1.7.0) |2016년 4월 26일 |--- |
| [1.6.3](#1.6.3) |2016년 4월 8일 |--- |
| [1.6.2](#1.6.2) |2016년 3월 29일 |--- |
| [1.5.3](#1.5.3) |2016년 2월 19일 |--- |
| [1.5.2](#1.5.2) |2015년 12월 14일 |--- |
| [1.5.1](#1.5.1) |2015년 11월 23일 |--- |
| [1.5.0](#1.5.0) |2015년 10월 5일 |--- |
| [1.4.1](#1.4.1) |2015년 8월 25일 |--- |
| [1.4.0](#1.4.0) |2015년 8월 13일 |--- |
| [1.3.0](#1.3.0) |2015년 8월 5일 |--- |
| [1.2.0](#1.2.0) |2015년 7월 6일 |--- |
| [1.1.0](#1.1.0) |2015년 4월 30일 |--- |
| [1.0.0](#1.0.0) |2015년 4월 8일 |--- |


## <a name="faq"></a>FAQ
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>참고 항목
Cosmos DB에 대해 자세히 toolearn 참조 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지. 


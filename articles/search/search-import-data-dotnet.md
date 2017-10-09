---
title: "aaa \"(.NET-Azure 검색) 데이터 업로드 | \"Microsoft Docs"
description: "Tooupload 데이터 tooan 인덱스에서 사용 하 여 Azure 검색.NET SDK hello 하는 방법에 대해 알아봅니다."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a>.NET SDK hello 업로드 데이터 tooAzure 사용 하 여 검색
> [!div class="op_single_selector"]
> * [개요](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST (영문)](search-import-data-rest-api.md)
> 
> 

이 문서에서는 보여 어떻게 toouse hello [Azure 검색.NET SDK](https://aka.ms/search-sdk) tooimport 데이터를 Azure 검색 인덱스입니다.

이 연습을 시작하기 전에 [Azure 검색 인덱스를 만들어야](search-what-is-an-index.md)합니다. 이 문서도 이미 만들었다고 가정는 `SearchServiceClient` 같이 개체 [hello.NET SDK를 사용 하 여 Azure 검색 인덱스를 만들](search-create-index-dotnet.md#CreateSearchServiceClient)합니다.

> [!NOTE]
> 이 문서의 모든 샘플 코드는 C#으로 작성되었습니다. Hello 전체 소스 코드를 찾을 수 [GitHub에서](http://aka.ms/search-dotnet-howto)합니다. Hello에 대 한 읽을 수 있습니다 [Azure 검색.NET SDK](search-howto-dotnet-sdk.md) hello 샘플 코드의 자세한 연습 과정에 대 한 합니다.

Hello.NET SDK를 사용 하 여 인덱스로 toopush 문서 순서에서에서 해야 합니다.

1. 만들기는 `SearchIndexClient` 개체 tooconnect tooyour 검색 인덱스입니다.
2. 만들기는 `IndexBatch` hello 문서 toobe 포함 된 추가, 수정 또는 삭제 합니다.
3. Hello 호출 `Documents.Index` 방식의 프로그램 `SearchIndexClient` toosend hello `IndexBatch` tooyour 검색 인덱스입니다.

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Hello SearchIndexClient 클래스의 인스턴스를 만들으십시오
tooimport 데이터를 사용 하 여 인덱스를 hello Azure 검색.NET SDK에서는 toocreate hello의 인스턴스를 만들어야 합니다 `SearchIndexClient` 클래스입니다. 생성할 수 있습니다이 인스턴스를 직접 하지만 쉽게 이미 있는 경우는 `SearchServiceClient` 인스턴스 toocall 해당 `Indexes.GetClient` 메서드. 예를 들어, 가져오는 것 방법을 다음은 한 `SearchIndexClient` 에서 "호텔" 이라는 hello 인덱스에 대 한는 `SearchServiceClient` 라는 `serviceClient`:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> 일반적인 검색 응용 프로그램에서 인덱스 관리 및 채우기는 검색 쿼리와는 별도의 구성 요소에 의해 처리됩니다. `Indexes.GetClient`저장 하기 때문에 인덱스를 채우는 편리한 다른를 제공 하는 데 문제가 hello `SearchCredentials`합니다. 해당 하면 사용한 toocreate hello hello 관리자 키를 전달 하 여 이렇게 `SearchServiceClient` 새 toohello `SearchIndexClient`합니다. 그러나 쿼리를 실행 하는 응용 프로그램 부분에서는 hello, 것이 더 나은 toocreate hello `SearchIndexClient` 직접 관리자 키 대신 쿼리 키에 전달할 수 있도록 합니다. 이 hello와 일치 [최소 권한의 원칙](https://en.wikipedia.org/wiki/Principle_of_least_privilege) toomake 보다 안전한 응용 프로그램 도움이 됩니다. 관리자 키 및 쿼리 키 hello에 대 한 자세한 내용을 확인할 수 [Azure 검색 REST API 참조](https://docs.microsoft.com/rest/api/searchservice/)합니다.
> 
> 

`SearchIndexClient`에는 `Documents` 속성이 있습니다. 이 속성 수정, 삭제 또는 인덱스의 문서를 쿼리 tooadd, 필요한 모든 hello 메서드를 제공 합니다.

## <a name="decide-which-indexing-action-toouse"></a>인덱싱 동작 toouse 결정
hello.NET SDK를 사용 하 여 tooimport 데이터, 해야 toopackage에 데이터를는 `IndexBatch` 개체입니다. `IndexBatch` 의 컬렉션을 캡슐화 `IndexAction` 각각 포함 하는 문서와 Azure 검색 어떤 작업 tooperform (업로드, 병합, 삭제 등)에 해당 문서에 지시 하는 속성 개체입니다. Hello 아래의 선택한 작업 중 어느 것을 따라 특정 필드만 각 문서에 포함 되어야 합니다.

| 동작 | 설명 | 각 문서에 대해 필요한 필드 | 참고 사항 |
| --- | --- | --- | --- |
| `Upload` |`Upload` 동작은 비슷한 tooan hello 문서를 새이 경우 삽입 및 업데이트/교체 있는 경우 하려는 "upsert"입니다. |키와, toodefine를 원하는 다른 모든 필드 |기존 문서를 업데이트/교체 hello 요청에 지정 되지 않은 모든 필드 갖게 되며 해당 필드가 너무 설정`null`합니다. Hello 필드 tooa null이 아닌 값을 이전에 설정 된 경우에 발생 합니다. |
| `Merge` |업데이트 hello를 사용 하 여 문서에서 기존 필드를 지정 합니다. Hello 문서 hello 인덱스에 없는 경우 hello 병합 하지 못합니다. |키와, toodefine를 원하는 다른 모든 필드 |병합에서 지정 하는 필드로 hello hello 문서의 기존 필드를 바뀝니다. 여기에는 `DataType.Collection(DataType.String)`형식 필드가 포함됩니다. 예를 들어 경우 hello 문서는 필드가 `tags` 값으로 `["budget"]` 값과 병합을 실행 하 고 `["economy", "pool"]` 에 대 한 `tags`, hello의 최종 값 hello `tags` 필드가 `["economy", "pool"]`합니다. `["budget", "economy", "pool"]`이 아닙니다. |
| `MergeOrUpload` |이 작업 처럼 동작 `Merge` hello 키를 이미 제공 하 여 문서 hello 인덱스에 있는 경우. 처럼 동작 하는 hello 문서가 없는 경우 `Upload` 새 문서를 사용 합니다. |키와, toodefine를 원하는 다른 모든 필드 |- |
| `Delete` |Hello 인덱스에서 hello 지정 된 문서를 제거합니다. |키만 |Hello 키 필드를 무시 것과 다른 모든 필드 지정 합니다. 문서에서 개별 필드 tooremove 사용 `Merge` 대신 하 고 간단 하 게 hello 필드를 명시적으로 설정 toonull 합니다. |

와 toouse 원하는 어떤 작업을 지정할 수 있습니다 hello의 다양 한 정적 메서드를 hello `IndexBatch` 및 `IndexAction` hello 다음 섹션에 나와 있는 것 처럼 클래스입니다.

## <a name="construct-your-indexbatch"></a>IndexBatch 생성
준비 tooconstruct hello는 문서에는 작업 tooperform를 파악 했으므로 `IndexBatch`합니다. 다음 예제에서는 어떻게 hello toocreate 몇 가지 다른 동작이 포함 된 일괄 처리 합니다. 예에서 사용 하 라는 사용자 지정 클래스 `Hotel` tooa 문서 hello "호텔" 인덱스에 매핑하는 합니다.

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "1",
                BaseRate = 199.0,
                Description = "Best hotel in town",
                DescriptionFr = "Meilleur hôtel en ville",
                HotelName = "Fancy Stay",
                Category = "Luxury",
                Tags = new[] { "pool", "view", "wifi", "concierge" },
                ParkingIncluded = false,
                SmokingAllowed = false,
                LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero),
                Rating = 5,
                Location = GeographyPoint.Create(47.678581, -122.131577)
            }),
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "2",
                BaseRate = 79.99,
                Description = "Cheapest hotel in town",
                DescriptionFr = "Hôtel le moins cher en ville",
                HotelName = "Roach Motel",
                Category = "Budget",
                Tags = new[] { "motel", "budget" },
                ParkingIncluded = true,
                SmokingAllowed = true,
                LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
                Rating = 1,
                Location = GeographyPoint.Create(49.678581, -122.131577)
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

사용 하 여이 경우 `Upload`, `MergeOrUpload`, 및 `Delete` hello에서 호출 하는 hello 메서드에 의해 지정 된 대로 우리의 검색 동작, `IndexAction` 클래스입니다.

이 예제 "호텔" 인덱스는 문서 수로 채워진다고 가정합니다. 어떻게 없는 toospecify hello 가능한 문서 필드를 모두 사용 하는 경우 유의 `MergeOrUpload` 어떻게 hello 문서 키만 지정 하 고 (`HotelId`) 사용 하는 경우 `Delete`합니다.

또한, 이때 인덱싱 단일 요청에서 too1000 문서를 포함할 수 있습니다.

> [!NOTE]
> 이 예제에서는 다양 한 작업 toodifferent 문서 적용 중인 합니다. 호출 하는 대신 hello 일괄 처리의 모든 문서 전체 tooperform 동일한 동작 hello 하려는 경우 `IndexBatch.New`, 사용할 수 있습니다의 다른 정적 메서드를 hello `IndexBatch`합니다. 예를 들어 `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` 또는 `IndexBatch.Delete`를 호출하여 배치를 만들 수 있습니다. 이러한 메서드는 `IndexAction` 개체 대신 문서의 컬렉션을 가져옵니다(이 예제에서 `Hotel` 유형의 개체).
> 
> 

## <a name="import-data-toohello-index"></a>가져오기 데이터 toohello 인덱스
초기화 된 했으므로 `IndexBatch` 개체를 호출 하 여 toohello 인덱스 보낼 수 있습니다 `Documents.Index` 에 프로그램 `SearchIndexClient` 개체입니다. hello 방법을 예제와 다음 toocall `Index`외에 일부 추가 단계가 tooperform 필요 합니다.

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
    // hello batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log hello failed document keys and continue.
    Console.WriteLine(
        "Failed tooindex some of hello documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents toobe indexed...\n");
Thread.Sleep(2000);
```

참고 hello `try` / `catch` hello 호출 toohello 주변 `Index` 메서드. hello catch 블록에서 인덱싱에 대 한 중요 한 오류 사례를 처리합니다. Azure 검색 서비스 tooindex hello의 일부 문서 hello 일괄 처리에 실패 하는 경우는 `IndexBatchException` 가 throw `Documents.Index`합니다. 이는 부하가 높은 상태에서 서비스되는 동안에 문서를 인덱싱하는 경우 발생할 수 있습니다. **이 경우 코드에서 명시적으로 처리하는 것이 좋습니다.** 지연 하 고, 실패 인덱싱 hello 문서를 다시 시도 하십시오 또는 로그 hello 예제에서는 하거나 응용 프로그램의 데이터 일관성 요구 사항에 따라 다른 작업을 수행할 수 있습니다를 계속할 수 있습니다.

마지막으로, hello 코드를 2 초 동안 지연 위의 hello 예제입니다. 인덱싱 발생 비동기적으로 Azure 검색 서비스에 hello 샘플 응용 프로그램 toowait hello 문서는 검색에 사용할 수 있는 짧은 시간 tooensure 해야 합니다. 이와 같이 데모, 테스트, 샘플 응용 프로그램에서는 일반적으로 지연만 필요합니다.

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a>Hello.NET SDK에서 문서를 처리 하는 방법
Hello Azure 검색.NET SDK와 같은 사용자 정의 클래스의 인스턴스 수 tooupload은 어떻게 할까요 `Hotel` toohello 인덱스입니다. toohelp 해당 질문에 답변을 사용 hello `Hotel` 클래스에 정의 된 toohello 인덱스 스키마에 매핑하는 [hello.NET SDK를 사용 하 여 Azure 검색 인덱스를 만들](search-create-index-dotnet.md#DefineIndex):

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }

    // ToString() method omitted for brevity...
}
```

hello 먼저 toonotice은 각 public 속성의 `Hotel` tooa 필드 hello 인덱스 정의의 하지만 한 가지 중요 한 차이점은 해당: hello 이름은 각 공용 동안 소문자 ("카멜식 대 /")으로 시작 하는 각 필드의 hello 이름 속성의 `Hotel` 대문자 문자 ("파스칼식 대 / 소문자로")로 시작 합니다. 여기서 hello 대상 스키마는 hello 응용 프로그램 개발자의 외부 hello 제어 데이터 바인딩을 수행 하는.NET 응용 프로그램에서 일반적인 시나리오입니다. 속성 이름은 카멜식 대 / 소문자를 늘려 명명 지침 tooviolate hello.NET 대신 hello SDK toomap hello 속성 이름은 toocamel 사례 hello로 자동으로 알 수 있습니다 `[SerializePropertyNamesAsCamelCase]` 특성입니다.

> [!NOTE]
> Azure 검색.NET SDK hello hello를 사용 하 여 [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) 라이브러리 tooserialize 하 고 사용자 사용자 지정 모델 개체 tooand JSON에서 역직렬화 합니다. 필요한 경우 직렬화를 사용자 지정할 수 있습니다. 자세한 내용은 [JSON.NET으로 직렬화 사용자 지정](search-howto-dotnet-sdk.md#JsonDotNet)를 참조하세요. 이 한 가지 예로 hello hello 사용 `[JsonProperty]` hello에 대 한 특성 `DescriptionFr` hello 위의 샘플 코드에는 속성입니다.
> 
> 

hello에 대 한 두 번째 중요 한 사항은 hello `Hotel` 클래스는 hello 공용 속성의 hello 데이터 형식입니다. 이러한 속성의 hello.NET 형식은 hello 인덱스 정의의 해당 필드 형식을 tootheir 매핑합니다. 예를 들어 hello `Category` 문자열 속성 매핑됩니다 toohello `category` 형식인 필드 `DataType.String`합니다. `bool?` 및 `DataType.Boolean`, `DateTimeOffset?` 및 `DataType.DateTimeOffset` 사이에는 유사한 유형 매핑이 있습니다. hello 형식 매핑에 대 한 특정 규칙 hello hello로 사항은 `Documents.Get` hello에 대 한 메서드 [Azure 검색.NET SDK 참조](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)합니다.

이 기능은 toouse 양방향;에서 작동 하는 문서로 서 사용자 고유의 클래스 또한 검색 결과 검색 하 고 수 hello SDK 자동으로 형식을 역직렬화 할에 tooa의 선택한 hello에 나와 있는 것 처럼 [다음 기사](search-query-dotnet.md)합니다.

> [!NOTE]
> hello Azure 검색.NET SDK에서는 hello를 사용 하 여 동적으로 입력 문서 `Document` 필드 이름 toofield 값의 키/값 매핑이 설정 되는 클래스입니다. 이 hello 인덱스 스키마 디자인 타임에 알 수 없는 하거나는 것이 불편 toobind toospecific 모델 클래스 시나리오에서 유용 합니다. Hello SDK의에서 문서를 처리 하는 모든 hello 메서드 hello를 사용 하는 오버 로드를 갖고 `Document` 클래스 뿐만 아니라 제네릭 형식 매개 변수를 사용 하는 강력한 형식의 오버 로드 합니다. 후자의 hello만이 문서에 hello 샘플 코드에 사용 됩니다.
> 
> 

**Null 허용 데이터 형식을 사용해야 하는 이유**

사용자 고유의 모델 클래스 toomap tooan Azure 검색 인덱스를 디자인할 때와 같은 값 형식의 속성을 선언 하는 것이 좋습니다 `bool` 및 `int` nullable toobe (예를 들어 `bool?` 대신 `bool`). Nullable이 아닌 속성을 사용 하면 있으면 너무**보장** 문서가 인덱스에는 hello 해당 필드에 대 한 null 값이 포함 됩니다. Hello SDK도 아니고 hello Azure 검색 서비스 할 수 있습니다 tooenforce이 있습니다.

이 가상의 중요 하지 않은 것: 있는 인덱스를 추가 하면 새 필드 tooan 기존 유형의 경우를 가정해 보십시오 `DataType.Int32`합니다. Hello 인덱스 정의 업데이트 한 후 모든 문서 (Azure 검색에서 null을 허용 하지 않는 형식도) 이후 해당 새 필드에 대해 null 값을 갖습니다. 다음으로 nullable이 아닌 모델 클래스를 사용 하는 경우 `int` 해당 필드에 대 한 속성을 얻게 됩니다는 `JsonSerializationException` tooretrieve 문서 하려고 할 때 다음과 같이 합니다.

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

이러한 이유로 모델 클래스에는 Null을 허용하는 형식을 사용하는 것이 가장 좋습니다.

## <a name="next-steps"></a>다음 단계
Azure 검색 인덱스를 채울 후 준비 toostart 문서에 대 한 쿼리 toosearch 발급 됩니다. 세부 정보는 [Azure 검색 인덱스 쿼리](search-query-overview.md) 를 참조하세요.


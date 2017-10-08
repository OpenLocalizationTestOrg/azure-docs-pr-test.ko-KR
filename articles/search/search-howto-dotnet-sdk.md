---
title: ".NET 응용 프로그램에서 Azure 검색 aaaHow toouse | Microsoft Docs"
description: ".NET 응용 프로그램에서 toouse Azure 검색 하는 방법"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a>.NET 응용 프로그램에서 toouse Azure 검색 하는 방법
이 문서는 연습 tooget hello로 실행 하면 [Azure 검색.NET SDK](https://aka.ms/search-sdk)합니다. 다양 한 기능의 hello.NET SDK tooimplement를 사용할 수 있습니다 Azure 검색을 사용 하 여 응용 프로그램에서 경험을 검색 합니다.

## <a name="whats-in-hello-azure-search-sdk"></a>무엇이 hello Azure 검색 SDK
hello SDK 이루어져 클라이언트 라이브러리 `Microsoft.Azure.Search`합니다. 인덱스, 데이터 원본 및 인덱서 toomanage 있습니다를 사용 하면으로 업로드 및 문서를 관리 하 고 HTTP 및 JSON hello 세부 정보와 함께 toodeal 필요 없이 모든 쿼리를 실행 합니다.

hello 클라이언트 라이브러리와 같은 클래스를 정의 `Index`, `Field`, 및 `Document`뿐만 아니라 등의 작업 `Indexes.Create` 및 `Documents.Search` hello에 `SearchServiceClient` 및 `SearchIndexClient` 클래스입니다. 이러한 클래스는 hello 네임 스페이스를 다음으로 구성 되어 있습니다.

* [Microsoft.Azure.Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [Microsoft.Azure.Search.Models](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

hello 현재 버전의 Azure 검색.NET SDK hello 일반적으로 출시 되었습니다. Tooprovide 피드백 원하는 경우 우리 tooincorporate hello 다음 버전의를 참조 하십시오 우리의 [피드백 페이지](https://feedback.azure.com/forums/263029-azure-search/)합니다.

hello.NET SDK 버전을 지원 `2016-09-01` 의 hello [Azure 검색 REST API](https://docs.microsoft.com/rest/api/searchservice/)합니다. 이 버전에서 이제 사용자 지정 분석기와 Azure Blob 및 Azure 테이블 인덱서를 지원합니다. 미리 보기 기능이 있는 *하지* JSON 및 CSV 파일에 대 한 지원 등이 버전의 일부에 있는 [미리 보기](search-api-2015-02-28-preview.md) 되 고 이전 hello를 통해 사용 가능한 [2.0-미리 보기 버전의.NET SDK hello ](https://aka.ms/search-sdk-preview).

이 SDK는 Search 서비스 생성 및 확장, API 키 관리 등의 [관리 작업](https://docs.microsoft.com/rest/api/searchmanagement/)을 지원하지 않습니다. .NET 응용 프로그램에서 리소스를 검색 toomanage 해야 할 경우 hello를 사용할 수 있습니다 [Azure 검색.NET 관리 SDK](https://aka.ms/search-mgmt-sdk)합니다.

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a>Toohello hello SDK의 최신 버전 업그레이드
이전 버전의 hello Azure 검색.NET SDK를 이미 사용 중이 고 tooupgrade toohello 새 일반 공급 버전을 선택 하는 경우 [이 문서](search-dotnet-sdk-migration.md) 설명 방법입니다.

## <a name="requirements-for-hello-sdk"></a>Hello SDK에 대 한 요구 사항
1. Visual Studio 2017.
2. Azure 검색 서비스 순서 toouse hello SDK, 서비스의 hello 이름과 API 키를 하나 이상 필요 합니다. [Hello 포털에 서비스를 만들](search-create-service-portal.md) 이러한 단계를 수 있습니다.
3. Hello Azure 검색.NET SDK를 다운로드 [NuGet 패키지](http://www.nuget.org/packages/Microsoft.Azure.Search) Visual Studio에서 "NuGet 패키지 관리"를 사용 하 여 합니다. 방금 hello 패키지 이름에 대 한 검색 `Microsoft.Azure.Search` NuGet.org에 있습니다.

Azure 검색.NET SDK hello hello.NET Framework 4.6 및.NET Core를 대상으로 하는 응용 프로그램을 지원 합니다.

## <a name="core-scenarios"></a>핵심 시나리오
몇 가지 방법으로 toodo 검색 응용 프로그램에 필요 합니다. 이 자습서에서는 이러한 핵심 시나리오를 다룹니다.

* 인덱스 만들기
* 문서와 함께 hello 인덱스 채우기
* 전체 텍스트 검색 및 필터를 사용하여 문서 검색하기

hello 다음 예제 코드에서는 이러한 각 보여 줍니다. 사용자의 응용 프로그램에서 무료 toouse hello 코드 조각을 느낍니다.

### <a name="overview"></a>개요
hello 살펴보겠습니다 샘플 응용 프로그램에서는 새 "호텔" 라는 인덱스 몇 가지 문서와 함께 정보를 표시 한 후 일부 검색 쿼리를 실행 합니다. 다음을 보여 주는 hello 주 프로그램은 전체 흐름 hello:

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> 이 연습 과정에서 사용 되는 hello 샘플 응용 프로그램의 hello 전체 소스 코드를 찾을 수 [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)합니다.
> 
>

단계별로 연습해보겠습니다. 먼저 새 toocreate 해야 `SearchServiceClient`합니다. 이 개체 toomanage 인덱스가 있습니다. 하나 순서 tooconstruct, Azure 검색 서비스 이름 뿐만 아니라 관리자 API 키 tooprovide 필요 합니다. Hello에이 정보를 입력할 수 있습니다 `appsettings.json` 파일의 hello [샘플 응용 프로그램](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)합니다.

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> 잘못 된 키 (예를 들어 관리자 키가 필요 하는 쿼리 키)를 제공 하는 경우 hello `SearchServiceClient` throw 됩니다는 `CloudException` hello 오류 메시지 "금지 된" hello로 처음으로 작업에서 메서드를 호출,와 같은 `Indexes.Create`합니다. 이런 경우가 발생 tooyou 우리의 API 키를 다시 확인 하십시오.
> 
> 

hello 다음 몇 줄만 작성 호출 메서드 toocreate 이미 있는 경우 먼저 삭제 "호텔" 라는 인덱스입니다. 잠시 후 이들 메서드를 연습해보겠습니다.

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

다음으로 hello 인덱스 toobe 채워져 있어야 합니다. toodo이 필요 합니다는 `SearchIndexClient`합니다. 하나는 두 가지 방법 tooobtain 가지:를 호출 하거나, 구성 하 여 `Indexes.GetClient` hello에 `SearchServiceClient`합니다. 후자의 hello 편의 위해 사용합니다.

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> 일반적인 검색 응용 프로그램에서 인덱스 관리 및 채우기는 검색 쿼리와는 별도의 구성 요소에 의해 처리됩니다. `Indexes.GetClient`저장 하기 때문에 인덱스를 채우는 편리한 다른를 제공 하는 데 문제가 hello `SearchCredentials`합니다. 해당 하면 사용한 toocreate hello hello 관리자 키를 전달 하 여 이렇게 `SearchServiceClient` 새 toohello `SearchIndexClient`합니다. 그러나 쿼리를 실행 하는 응용 프로그램 부분에서는 hello, 것이 더 나은 toocreate hello `SearchIndexClient` 직접 관리자 키 대신 쿼리 키에 전달할 수 있도록 합니다. 최소 권한의 원칙 hello와 일치 하 고 toomake 보다 안전한 응용 프로그램 도움이 됩니다. 관리 키와 쿼리 키에 대한 자세한 내용은 [여기](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization)에서 확인할 수 있습니다.
> 
> 

이제는 `SearchIndexClient`, hello 인덱스를 채울 수 있습니다. 이것은 나중에 연습할 또 다른 메서드에 의해 수행됩니다.

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

마지막으로, 몇 가지 검색 쿼리를 실행 하 고 hello 결과 표시 합니다. 이번에는 다른 `SearchIndexClient`를 사용할 것입니다.

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

이전 걸립니다 좀 더 자세히 살펴보고 hello `RunQueries` 나중 메서드. 여기서는 hello 코드 toocreate hello 새 `SearchIndexClient`:

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

이 시간 사용은 쿼리 키 이후 쓰기 액세스 toohello 인덱스가 필요 하지 않습니다. Hello에이 정보를 입력할 수 있습니다 `appsettings.json` 파일의 hello [샘플 응용 프로그램](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)합니다.

올바른 서비스 이름 및 API 키 사용이 응용 프로그램을 실행 하는 경우 hello 출력은 다음과 같이 표시 됩니다.

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

hello 응용 프로그램의 hello 전체 소스 코드는이 문서의 hello 끝에서 제공 됩니다.

다음으로, 각 hello 메서드에 의해 호출 자세히 보기 메뉴로 이동 합니다 `Main`합니다.

### <a name="creating-an-index"></a>인덱스 만들기
만든 후는 `SearchServiceClient`, hello 다음으로 `Main` 가 이미 있는 경우에 delete 호텔"hello" 인덱스입니다. 작업은 hello 메서드 뒤에 의해 수행 됩니다.

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

이 방법은 제공 하는 hello를 사용 하 여 `SearchServiceClient` toocheck hello 인덱스가 있는 경우 그리고 있다면 삭제 합니다.

> [!NOTE]
> hello 예제 코드에서는이 문서에 간단한 설명을 위해 hello Azure 검색.NET SDK의 hello 동기 메서드를 사용합니다. 사용자 고유의 응용 프로그램 tookeep에 hello 비동기 메서드를 사용 하는 것이 좋습니다 확장성과 응답성이 해당 합니다. 예를 들어 hello 있습니다 위의 메서드에서 사용 하 여 `ExistsAsync` 및 `DeleteAsync` 대신 `Exists` 및 `Delete`합니다.
> 
> 

그 다음 `Main`이(가) 이 메서드를 호출하여 새 "호텔" 인덱스를 만듭니다.

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

이 메서드가 만드는 새 `Index` 개체 목록이 `Field` hello 새 인덱스의 hello 스키마를 정의 하는 개체입니다. 각 필드에는 이름, 데이터 유형, 그리고 검색 동작을 정의하는 몇 가지 특성이 있습니다. hello `FieldBuilder` 클래스가 사용 하 여 리플렉션 toocreate 목록이 `Field` 제공 hello의 공용 속성 및 특성 개체를 검사 하 여 hello 인덱스에 대 한 hello `Hotel` 모델 클래스입니다. 좀 더 자세히 살펴보고 hello 살펴보겠습니다 `Hotel` 나중에 클래스입니다.

> [!NOTE]
> 항상 hello 목록을 만들 수 있습니다 `Field` 개체를 사용 하는 대신 직접 `FieldBuilder` 필요한 경우. 예를 들어 toouse 모델 클래스를 원하지 않을 수 있습니다 또는 toouse 않도록 toomodify 특성을 추가 하 여 기존 모델 클래스를 할 수 있습니다.
>
> 

또한 toofields를 추가할 수 있습니다도 점수 매기기 프로필, 확인 기, 또는 CORS 옵션 toohello 인덱스 (이러한 메서드 hello 샘플 코드에서 생략 됩니다). Hello에 hello Index 개체 및 해당 구성 요소에 대 한 자세한 정보를 찾을 수 [SDK 참조](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index)뿐만 아니라 hello 에서처럼에서 [Azure 검색 REST API 참조](https://docs.microsoft.com/rest/api/searchservice/)합니다.

### <a name="populating-hello-index"></a>Hello 인덱스 채우기
다음 단계를 hello `Main` toopopulate hello 새로 만든 인덱스입니다. 이 메서드를 다음 hello 작업 수행 됩니다.

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
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
        },
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
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

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
}
```

이 메서드는 네 부분으로 이루어져 있습니다. hello 먼저 이루어진 배열을 만들어 `Hotel` 우리의 입력된 데이터 tooupload toohello 인덱스 역할을 수행 하는 개체입니다. 이 데이터는 간단히 하기 위해 하드 코딩합니다. 사용 중인 응용 프로그램의 경우, 데이터는 SQL 데이터베이스와 같은 외부 데이터 원본에서 나올 가능성이 높습니다.

두 번째 부분 hello 만듭니다는 `IndexBatch` hello 문서가 들어 있는입니다. Hello 작업,이 경우 호출 하 여 만든 hello 시 tooapply toohello 일괄 처리를 원하는 지정 `IndexBatch.Upload`합니다. hello 일괄 처리는 hello 여 업로드 된 toohello Azure 검색 인덱스 다음 `Documents.Index` 메서드.

> [!NOTE]
> 이 예에서는 문서를 업로드하는 것입니다. Toomerge 기존 문서 또는 문서 삭제 포인터가 필요한 경우 일괄 처리를 호출 하 여 일으킬 `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, 또는 `IndexBatch.Delete` 대신 합니다. 또한 호출 하 여 단일 일괄 처리의 다른 작업을 혼합할 수 있습니다 `IndexBatch.New`, 컬렉션을 사용 하는 `IndexAction` Azure 검색 tooperform를 지시 하며 각 문서에 특정 작업 개체입니다. 각각 만들 수 있습니다 `IndexAction` 와 같은 hello 해당 메서드를 호출 하 여 자체 작업과 `IndexAction.Merge`, `IndexAction.Upload`등입니다.
> 
> 

이 메서드의 세 번째 부분은 hello는 인덱싱에 대 한 중요 한 오류 사례를 처리 하는 catch 블록입니다. Azure 검색 서비스 tooindex hello의 일부 문서 hello 일괄 처리에 실패 하는 경우는 `IndexBatchException` 가 throw `Documents.Index`합니다. 이는 부하가 높은 상태에서 서비스되는 동안에 문서를 인덱싱하는 경우 발생할 수 있습니다. **이 경우 코드에서 명시적으로 처리하는 것이 좋습니다.** 지연 하 고, 실패 인덱싱 hello 문서를 다시 시도 하십시오 또는 로그 hello 예제에서는 하거나 응용 프로그램의 데이터 일관성 요구 사항에 따라 다른 작업을 수행할 수 있습니다를 계속할 수 있습니다.

> [!NOTE]
> Hello를 사용할 수 있습니다 `FindFailedActionsToRetry` 메서드 tooconstruct 포함 하는 새 일괄 처리에만 너무 한 이전 호출에 실패 한 작업 hello`Index`합니다. hello 메서드는 문서화 [여기](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) tooproperly 사용 하는 방법에 대 한 내용은 이며 [StackOverflow에](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry)합니다.
>
>

마지막으로, hello `UploadDocuments` 2 초에 대 한 메서드 지연이 발생 합니다. 인덱싱 발생 비동기적으로 Azure 검색 서비스에 hello 샘플 응용 프로그램 toowait hello 문서는 검색에 사용할 수 있는 짧은 시간 tooensure 해야 합니다. 이와 같이 데모, 테스트, 샘플 응용 프로그램에서는 일반적으로 지연만 필요합니다.

#### <a name="how-hello-net-sdk-handles-documents"></a>Hello.NET SDK에서 문서를 처리 하는 방법
Hello Azure 검색.NET SDK와 같은 사용자 정의 클래스의 인스턴스 수 tooupload은 어떻게 할까요 `Hotel` toohello 인덱스입니다. toohelp 해당 질문에 답변을 사용 hello `Hotel` 클래스:

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
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
}
```

hello 먼저 toonotice은 각 public 속성의 `Hotel` tooa 필드 hello 인덱스 정의의 하지만 한 가지 중요 한 차이점은 해당: hello 이름은 각 공용 동안 소문자 ("카멜식 대 /")으로 시작 하는 각 필드의 hello 이름 속성의 `Hotel` 대문자 문자 ("파스칼식 대 / 소문자로")로 시작 합니다. 여기서 hello 대상 스키마는 hello 응용 프로그램 개발자의 외부 hello 제어 데이터 바인딩을 수행 하는.NET 응용 프로그램에서 일반적인 시나리오입니다. 속성 이름은 카멜식 대 / 소문자를 늘려 명명 지침 tooviolate hello.NET 대신 hello SDK toomap hello 속성 이름은 toocamel 사례 hello로 자동으로 알 수 있습니다 `[SerializePropertyNamesAsCamelCase]` 특성입니다.

> [!NOTE]
> Azure 검색.NET SDK hello hello를 사용 하 여 [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) 라이브러리 tooserialize 하 고 사용자 사용자 지정 모델 개체 tooand JSON에서 역직렬화 합니다. 필요한 경우 직렬화를 사용자 지정할 수 있습니다. 자세한 내용은 [JSON.NET으로 직렬화 사용자 지정](#JsonDotNet)를 참조하세요.
> 
> 

hello 두 번째 작업 toonotice hello 특성 같은 `IsFilterable`, `IsSearchable`, `Key`, 및 `Analyzer` 각 공용 속성이 있는 장식 합니다. 이러한 특성 매핑 toohello 직접 [hello Azure 검색 인덱스의 해당 특성](https://docs.microsoft.com/rest/api/searchservice/create-index#request)합니다. hello `FieldBuilder` 클래스가 이러한 tooconstruct 필드 정의 사용 하 여 hello 인덱스에 대 한 합니다.

hello에 대 한 세 번째 중요 한 사항은 hello `Hotel` 클래스는 hello 공용 속성의 hello 데이터 형식입니다. 이러한 속성의 hello.NET 형식은 hello 인덱스 정의의 해당 필드 형식을 tootheir 매핑합니다. 예를 들어 hello `Category` 문자열 속성 매핑됩니다 toohello `category` 형식인 필드 `Edm.String`합니다. 간의 비슷한 형식 매핑을 `bool?` 및 `Edm.Boolean`, `DateTimeOffset?` 및 `Edm.DateTimeOffset`, 등 hello hello 형식 매핑에 대 한 특정 규칙 hello로 사항은 `Documents.Get` hello에 대 한 메서드 [Azure 검색.NET SDK 참조](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)합니다. hello `FieldBuilder` 클래스를이 매핑의 담당 것은 아니지만 수 여전히 도움이 toounderstand serialization 문제 tootroubleshoot 해야 할 경우.

이 기능은 toouse 양방향;에서 작동 하는 문서로 서 사용자 고유의 클래스 또한 검색 결과 검색 하 고 수 hello SDK 자동으로 형식을 역직렬화 할에 tooa의 선택한 hello 다음 섹션에 나와 있듯이 합니다.

> [!NOTE]
> hello Azure 검색.NET SDK에서는 hello를 사용 하 여 동적으로 입력 문서 `Document` 필드 이름 toofield 값의 키/값 매핑이 설정 되는 클래스입니다. 이 hello 인덱스 스키마 디자인 타임에 알 수 없는 하거나는 것이 불편 toobind toospecific 모델 클래스 시나리오에서 유용 합니다. Hello SDK의에서 문서를 처리 하는 모든 hello 메서드 hello를 사용 하는 오버 로드를 갖고 `Document` 클래스 뿐만 아니라 제네릭 형식 매개 변수를 사용 하는 강력한 형식의 오버 로드 합니다. 이 자습서에서는 hello 샘플 코드에서 hello 후자만 사용 됩니다. hello `Document` 클래스에서 상속 `Dictionary<string, object>`합니다. 자세한 내용은 [여기](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document)에서 확인할 수 있습니다.
> 
> 

**Null 허용 데이터 형식을 사용해야 하는 이유**

사용자 고유의 모델 클래스 toomap tooan Azure 검색 인덱스를 디자인할 때와 같은 값 형식의 속성을 선언 하는 것이 좋습니다 `bool` 및 `int` nullable toobe (예를 들어 `bool?` 대신 `bool`). Nullable이 아닌 속성을 사용 하면 있으면 너무**보장** 문서가 인덱스에는 hello 해당 필드에 대 한 null 값이 포함 됩니다. Hello SDK도 아니고 hello Azure 검색 서비스 할 수 있습니다 tooenforce이 있습니다.

이 가상의 중요 하지 않은 것: 있는 인덱스를 추가 하면 새 필드 tooan 기존 유형의 경우를 가정해 보십시오 `Edm.Int32`합니다. Hello 인덱스 정의 업데이트 한 후 모든 문서 (Azure 검색에서 null을 허용 하지 않는 형식도) 이후 해당 새 필드에 대해 null 값을 갖습니다. 다음으로 nullable이 아닌 모델 클래스를 사용 하는 경우 `int` 해당 필드에 대 한 속성을 얻게 됩니다는 `JsonSerializationException` tooretrieve 문서 하려고 할 때 다음과 같이 합니다.

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

이러한 이유로 모델 클래스에는 Null을 허용하는 형식을 사용하는 것이 가장 좋습니다.

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a>JSON.NET으로 직렬화 사용자 지정
hello SDK JSON.NET을 사용 하 여 직렬화 및 문서를 역직렬화 합니다. 직렬화를 사용자 지정할 수 있으며 필요한 경우를 정의 하 여 사용자 고유의 deserialization `JsonConverter` 또는 `IContractResolver` (hello 참조 [JSON.NET 설명서](http://www.newtonsoft.com/json/help/html/Introduction.htm) 자세한 세부 정보에 대 한). Azure 검색 및 기타 고급 시나리오에 사용할 응용 프로그램에서 tooadapt 기존 모델 클래스를 사용 하려는 경우에 유용할 수 있습니다. 예를 들어 사용자 지정 serialization으로 다음을 수행할 수 있습니다.

* 모델 클래스의 특정 속성을 문서 필드로 저장하는 데 포함 또는 제외할 수 있습니다.
* 코드의 속성 이름과 인덱스의 필드 이름을 매핑할 수 있습니다.
* 매핑 속성 toodocument 필드에 사용할 수 있는 사용자 지정 특성을 만듭니다.

GitHub의 Azure 검색.NET SDK hello에 대 한 hello 단위 테스트에서 사용자 지정 직렬화를 구현의 예를 찾을 수 있습니다. 적절한 시작 지점은 [이 폴더](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models)입니다. Hello 사용자 지정 직렬화 테스트에서 사용 되는 클래스를 포함 합니다.

### <a name="searching-for-documents-in-hello-index"></a>Hello 인덱스의 문서에 대 한 검색
hello hello 샘플 응용 프로그램의 마지막 단계는 toosearch hello 인덱스의 일부 문서에 대 한 합니다. hello 메서드 뒤이 수행 합니다.

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
    Console.WriteLine("lastRenovationDate:\n");

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

쿼리를 실행할 때마다 이 메서드는 먼저 새 `SearchParameters` 개체를 만듭니다. 사용 되는 toospecify 정렬, 필터링, 페이징, 패싯 등 hello 쿼리에 대 한 추가 옵션입니다. 이 방법에서는 hello 설정 하 고 `Filter`, `Select`, `OrderBy`, 및 `Top` 다른 쿼리에 대 한 속성입니다. 모든 hello `SearchParameters` 속성 설명 [여기](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters)합니다.

hello 다음 단계는 tooactually hello 검색 쿼리를 실행 합니다. 이 작업은 수행 hello를 사용 하 여 `Documents.Search` 메서드. 각 쿼리에 대 한 문자열 hello 검색 텍스트 toouse 전달 (또는 `"*"` 없는 검색 텍스트가 있는 경우), 플러스 hello 앞에서 만든 매개 변수를 검색 합니다. 또한 지정 `Hotel` 에 대 한 형식 매개 변수와 hello `Documents.Search`, 형식의 개체에 hello SDK toodeserialize 문서 hello 검색 결과에 지시 `Hotel`합니다.

> [!NOTE]
> Hello 검색 쿼리 식 구문에 대 한 자세한 정보를 찾을 수 [여기](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search)합니다.
> 
> 

마지막으로, 각 쿼리 한 후이 메서드를 통해 모든 hello hello 검색 결과에서 각 문서 toohello 콘솔 인쇄 반복:

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

자세히 보기의 각 hello 쿼리를 다시 보겠습니다. Hello 코드 tooexecute hello 첫 번째 쿼리는 다음과 같습니다.

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

이 경우에서는 hello 단어 "budget"와 일치 하는 호텔 검색할 하 고 tooget 다시 hello 호텔 이름만, hello에 지정 된 대로 원하는 `Select` 매개 변수입니다. Hello 결과 다음과 같습니다.

    Name: Roach Motel

다음으로 야간 보다 작은 $150, 속도가 toofind hello 호텔 원하는 하 고 hello 호텔 ID와 설명을 반환:

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

이 쿼리는 OData를 사용 하 여 `$filter` 식 `baseRate lt 150`, hello 인덱스의 toofilter hello 문서. Azure 검색에서 지 원하는 OData 구문 hello에 대 한 자세한 내용을 확인할 수 [여기](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search)합니다.

Hello hello 쿼리 결과 다음과 같습니다.

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

다음으로, toofind hello 상위 두 호텔 가장 최근에 리 모델링 되었고, 고 hello 호텔 이름 및 보수의 마지막 날짜를 보여 주는 주시기 바랍니다. Hello 코드는 다음과 같습니다. 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

이 경우에서는 다시 사용 하 여 OData 구문을 toospecify hello `OrderBy` 매개 변수로 `lastRenovationDate desc`합니다. 또한 설정 `Top` too2 tooensure만 얻을 수 있는 hello 상위 두 문서입니다. 설정 하 여 이전 처럼 `Select` toospecify 필드를 반환 합니다.

Hello 결과 다음과 같습니다.

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

마지막으로, toofind hello 단어 "motel"와 일치 하는 모든 호텔 원하는:

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

다음은 hello를 지정 하지 않았기 때문에 모든 필드를 포함 하는 hello 결과 및 `Select` 속성:

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

이 단계는 hello 자습서를 완료 하지만 보십시오. **다음 단계** 에서는 Azure 검색에 대해 자세히 학습하기 위한 추가 리소스가 제공됩니다.

## <a name="next-steps"></a>다음 단계
* Hello에 대 한 hello 참조 찾아보기 [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) 및 [REST API](https://docs.microsoft.com/rest/api/searchservice/)합니다.
* [비디오와 기타 샘플 및 자습서](search-video-demo-tutorial-list.md)를 통해 지식을 심화시키십시오.
* 검토 [명명 규칙](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello 규칙의 다양 한 개체 이름을 지정 합니다.
* Azure 검색에서 [지원되는 데이터 유형](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) 을 검토하십시오.

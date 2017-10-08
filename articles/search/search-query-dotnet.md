---
title: "aaa \"는 인덱스 (.NET API-Azure 검색) 쿼리하여 | \"Microsoft Docs"
description: "Azure 검색에서 검색 쿼리를 작성 하 고 검색 매개 변수 toofilter 및 정렬 검색 결과 사용 합니다."
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a>Hello.NET SDK를 사용 하 여 Azure 검색 인덱스를 쿼리 합니다.
> [!div class="op_single_selector"]
> * [개요](search-query-overview.md)
> * [포털](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST (영문)](search-query-rest-api.md)
> 
> 

이 문서에서는 보여 방법을 사용 하 여 인덱스 tooquery hello [Azure 검색.NET SDK](https://aka.ms/search-sdk)합니다.

이 연습을 시작하기 전에 [Azure 검색 인덱스를 만들고](search-what-is-an-index.md) [데이터로 채워야](search-what-is-data-import.md) 합니다.

> [!NOTE]
> 이 문서의 모든 샘플 코드는 C#으로 작성되었습니다. Hello 전체 소스 코드를 찾을 수 [GitHub에서](http://aka.ms/search-dotnet-howto)합니다. Hello에 대 한 읽을 수 있습니다 [Azure 검색.NET SDK](search-howto-dotnet-sdk.md) hello 샘플 코드의 자세한 연습 과정에 대 한 합니다.

## <a name="identify-your-azure-search-services-query-api-key"></a>Azure 검색 서비스의 쿼리 API 키 식별
Azure 검색 인덱스를 만들면 했으므로 hello.NET SDK를 사용 하 여 것 같군요 tooissue 쿼리 됩니다. 첫째, tooobtain hello 쿼리 api-key 생성 된 중 하나를 프로 비전 할 hello 검색 서비스에 대해 필요 합니다. hello.NET SDK는 모든 요청 tooyour 서비스에서이 api 키를 전송 합니다. 유효한 키가 있는 hello 요청 보내기 hello 응용 프로그램 사이이 처리 하는 hello 서비스 요청 별로 신뢰를 설정 합니다.

1. toofind toohello에 로그인 하려면 서비스의 api 키 [Azure 포털](https://portal.azure.com/)
2. Tooyour Azure 검색 서비스 블레이드로 이동
3. Hello에 "키" 아이콘을 클릭

서비스에는 *관리 키* 및 *쿼리 키*가 있습니다.

* 기본 및 보조 *관리자 키는* hello 기능 toomanage hello 서비스 등 tooall 작업 대 한 모든 권한 부여를 만들고 인덱스, 인덱서 및 데이터 원본을 삭제 합니다. 두 가지 tooregenerate hello 기본 키, 그 반대의 경우 toouse hello에 대 한 보조 키를 계속할 수 있도록 합니다.
* 프로그램 *키 쿼리* tooindexes 읽기 전용 액세스 및 문서를 부여 하 고 일반적으로 분산된 tooclient 하는 응용 프로그램이 검색 요청을 실행 합니다.

Hello 인덱스는 쿼리를 위해 쿼리 키 중 하나를 사용할 수 있습니다. 쿼리에 대 한 관리자 키도 사용할 수 있지만이 더 잘 hello를 다음과 같이 응용 프로그램 코드의 쿼리 키를 사용 해야 [최소 권한의 원칙](https://en.wikipedia.org/wiki/Principle_of_least_privilege)합니다.

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Hello SearchIndexClient 클래스의 인스턴스를 만들으십시오
Azure 검색.NET SDK hello로 tooissue 쿼리, toocreate hello 인스턴스의 필요 합니다 `SearchIndexClient` 클래스입니다. 이 클래스에는 몇 가지 생성자가 있습니다. 검색 서비스 이름, 인덱스 이름, 원하는 hello 사용 및 `SearchCredentials` 매개 변수로 개체입니다. `SearchCredentials` 는 API 키를 래핑합니다.

아래 hello 코드에서는 새 `SearchIndexClient` hello "호텔" 인덱스에 대 한 (에서 만든 [hello.NET SDK를 사용 하 여 Azure 검색 인덱스를 만들](search-create-index-dotnet.md)) hello 검색 서비스 이름 및 hello 응용 프로그램의 구성에 저장 되어 있는 api 키에 대 한 값을 사용 하 여 파일 (`appsettings.json` hello hello 경우에서 [샘플 응용 프로그램](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

`SearchIndexClient`에는 `Documents` 속성이 있습니다. 이 속성은 모든 hello tooquery Azure 검색 인덱스를 해야 하는 방법을 제공 합니다.

## <a name="query-your-index"></a>인덱스 쿼리
Hello.NET SDK를 사용한 검색은을 호출 hello `Documents.Search` 메서드를 프로그램 `SearchIndexClient`합니다. 와 함께 hello 검색 텍스트를 포함 하는 몇 가지 매개 변수를 사용 하는이 메서드는 `SearchParameters` 사용된 toofurther 구체화 hello 쿼리 될 수 있는 개체입니다.

#### <a name="types-of-queries"></a>쿼리 유형
hello 2 주 [쿼리 유형에](search-query-overview.md#types-of-queries) 사용할지는 `search` 및 `filter`합니다. `search` 쿼리는 인덱스에서 모든 *검색 가능한* 필드에 대해 하나 이상의 단어를 검색합니다. `filter` 쿼리는 인덱스의 *필터링 가능한* 모든 필드에 걸쳐 부울 식을 계산합니다.

검색 및 필터를 둘 다 hello를 사용 하 여 수행 됩니다 `Documents.Search` 메서드. 검색 쿼리는 hello에 전달 될 수 `searchText` 매개 변수, 필터 식을 hello에 전달 될 수 하는 동안 `Filter` hello 속성 `SearchParameters` 클래스입니다. 검색을 하지 않고 toofilter 전달 `"*"` hello에 대 한 `searchText` 매개 변수입니다. 필터링을 하지 않고 toosearch hello 둡니다 `Filter` 속성을 설정된 또는 전달 하지 않는 한 `SearchParameters` 전혀 인스턴스.

#### <a name="example-queries"></a>예제 쿼리
다음 샘플 코드는 hello tooquery hello "호텔" 인덱스에 정의 된 몇 가지 방법을 보여 줍니다 [hello.NET SDK를 사용 하 여 Azure 검색 인덱스를 만들](search-create-index-dotnet.md#DefineIndex)합니다. Hello 검색 결과 함께 반환 하는 hello 문서의 hello의 인스턴스는 `Hotel` 클래스에 정의 된 [데이터 가져오기를 사용 하 여 Azure 검색.NET SDK hello](search-import-data-dotnet.md#HotelClass)합니다. 샘플 코드 hello를 사용 하는 `WriteDocuments` 메서드 toooutput hello 검색 결과 toohello 콘솔. 이 메서드는 hello 다음 섹션에 설명 되어 있습니다.

```csharp
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
```

## <a name="handle-search-results"></a>검색 결과 처리
hello `Documents.Search` 메서드가 반환 되는 `DocumentSearchResult` hello hello 쿼리 결과 포함 하는 개체입니다. 라는 메서드를 사용 하는 hello 이전 단원의 hello 예제 `WriteDocuments` toooutput hello 검색 결과 toohello 콘솔:

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

다음 hello 결과가 hello 이전 단원의 hello 쿼리에 대 한 가정 하면 호텔"hello" 인덱스에 hello 샘플 데이터로 채워지는 같은 것은 [데이터 가져오기를 사용 하 여 Azure 검색.NET SDK hello](search-import-data-dotnet.md):

```
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
```

위의 샘플 코드 hello hello 콘솔 toooutput 검색 결과 사용합니다. 마찬가지로 응용 프로그램에서 toodisplay 검색 결과 할 수 있습니다. 참조 [GitHub에이 샘플](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) toorender 검색 ASP.NET MVC 기반 웹 응용 프로그램에서 발생 하는 방법의 예입니다.


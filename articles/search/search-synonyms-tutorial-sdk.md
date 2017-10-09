---
title: "aaaSynonyms 미리 Azure 검색의 자습서 | Microsoft Docs"
description: "Azure 검색의 hello 동의어 미리 보기 기능 tooan 인덱스를 추가 합니다."
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a>Azure Search에 대한 동의어(미리 보기) C# 자습서

동의어는 의미가 동일한 toohello 입력된 용어를 것으로 간주 되는 용어에 대해 비교 하 여 쿼리를 확장 합니다. 예를 들어 hello 용어 "automobile" 또는 "vehicle"가 포함 된 "car 라는" toomatch 문서 좋습니다.

Azure Search에서 동의어는 동등한 용어를 연결하는 *매핑 규칙*을 통해 *동의어 맵*에 정의됩니다. 여러 동의어 지도 만들 지정, 서비스 전체 리소스 사용 가능한 tooany 인덱스로 게시 및 참조할 수 있는 하나의 toouse hello 필드 수준에서 합니다. 쿼리 시 또한 toosearching Azure 검색 인덱스는 동의어 맵에서 조회 hello 쿼리에 사용 되는 필드에 지정 된 경우.

> [!NOTE]
> hello 동의어 기능은 현재에 미리 보기 및 최신 미리 보기 API와 SDK 버전에서 지원만 hello (api 버전 = 2016-09-01-미리 보기, SDK 버전 4.x-미리 보기). 지금은 Azure Portal 지원이 없습니다. 미리 보기 API는 SLA가 적용되지 않으며 미리 보기 기능이 변경될 수 있으므로 프로덕션 응용 프로그램에서 사용하지 않는 것이 좋습니다.

## <a name="prerequisites"></a>필수 조건

자습서 요구 사항은 hello 다음과를 같습니다.

* [Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure Search 서비스](search-create-service-portal.md)
* [Microsoft.Azure.Search .NET 라이브러리의 미리 보기 버전](https://aka.ms/search-sdk-preview)
* [.NET 응용 프로그램에서 toouse Azure 검색 하는 방법](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a>개요

쿼리 및 후 동의어의 hello 값을 보여 줍니다. 이 자습서에서는 쿼리를 실행하고 샘플 인덱스에서 결과를 반환하는 샘플 응용 프로그램을 사용합니다. hello 샘플 응용 프로그램은 두 문서 채워진 "호텔" 라는 작은 인덱스를 만듭니다. hello 응용 프로그램에는 문제 안녕 같은 검색 한 다음 hello 동의어 기능을 사용 하면를 hello 인덱스에 나타나지 않는 구와 용어를 사용 하 여 검색 쿼리를 실행 합니다. 아래의 hello 코드 hello를 설명 합니다. 전체 흐름.

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
단계 toocreate hello 및 hello 샘플 인덱스를 채우지 설명 [toouse Azure.NET 응용 프로그램에서 검색 하는 방법](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)합니다.

## <a name="before-queries"></a>"이전" 쿼리

`RunQueriesWithNonExistentTermsInIndex`에서 "five star", "internet", "economy AND hotel"로 검색 쿼리를 실행했습니다.
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
Hello 다음과 같이 hello에서 먼저 출력 얻을 수 있도록 hello 용어를 포함 모두 hello 두 인덱싱된 문서 `RunQueriesWithNonExistentTermsInIndex`합니다.
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a>동의어 사용

동의어 사용은 2단계 프로세스입니다. 먼저 정의 म 및 동의어 규칙을 업로드 하 고 다음 필드 toouse을 구성을 합니다. hello 프로세스도 둘러싸여 `UploadSynonyms` 및 `EnableSynonymsInHotelsIndex`합니다.

1. 동의어 맵 tooyour 검색 서비스를 추가 합니다. `UploadSynonyms`, ' desc synonymmap' 우리의 동의어 맵에서 4 개의 규칙을 정의 하 고 업로드 toohello 서비스입니다.
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
동의어 맵 toohello 오픈 소스 표준을 따라야 합니다. `solr` 형식입니다. hello 형식에 대해서는 설명 [Azure 검색의 동의어](search-synonyms.md) hello 섹션 아래의 `Apache Solr synonym format`합니다.

2. Hello 인덱스 정의의 검색 가능 필드 toouse hello 동의어 지도 구성 합니다. `EnableSynonymsInHotelsIndex`, 두 개 필드에는 동의어 설정 `category` 및 `tags` hello 설정 하 여 `synonymMaps` hello의 속성 toohello 이름을 새로 동의어 지도 업로드 합니다.
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
동의어 맵을 추가하면 인덱스를 다시 작성하지 않아도 됩니다. 동의어 맵 tooyour 서비스를 추가할 수 있으며 모든 인덱스 toouse hello 새 동의어 map의 기존 필드 정의 수정 합니다. 새 특성의 hello 추가 인덱스 가용성에 영향을 주어에 있습니다. 번호 필드에 대 한 동의어를 사용 하지 않도록 설정에 마찬가지입니다. Hello 설정 하기만 하면 `synonymMaps` 속성 tooan 빈 목록입니다.
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a>"이전" 쿼리

Hello 동의어 지도 업로드 하 고 hello 인덱스는 업데이트 된 toouse hello 동의어 지도 후 두 번째로 hello `RunQueriesWithNonExistentTermsInIndex` 호출 hello 다음 출력:

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
hello 첫 번째 쿼리 찾습니다 hello hello 규칙에서 문서 `five star=>luxury`합니다. hello 두 번째 쿼리를 사용 하 여 hello 검색 확장 `internet,wifi` 셋째 모두를 사용 하 여 hello 및 `hotel, motel` 및 `economy,inexpensive=>budget` 일치 hello 문서를 찾는 데 합니다.

동의어를 완전히 추가 hello 검색 환경을 변경 됩니다. 이 자습서에서는 hello 원래 쿼리는 인덱스의 hello 문서 관련 된 경우에 tooreturn 의미 있는 결과 실패 했습니다. 동의어를 사용 하 여 hello 인덱스에서 변경 내용 toounderlying 데이터가 없는 용어에서 일반적으로 사용 하는 인덱스 tooinclude를 확장할 수 있습니다.

## <a name="sample-application-source-code"></a>샘플 응용 프로그램 소스 코드
이 연습 과정에서 사용 되는 hello 샘플 응용 프로그램의 hello 전체 소스 코드를 찾을 수 [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms)합니다.

## <a name="next-steps"></a>다음 단계

* 검토 [어떻게 Azure 검색의 toouse 동의어](search-synonyms.md)
* [동의어 REST API 설명서](https://aka.ms/rgm6rq) 검토
* Hello에 대 한 hello 참조 찾아보기 [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) 및 [REST API](https://docs.microsoft.com/rest/api/searchservice/)합니다.

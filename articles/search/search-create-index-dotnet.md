---
title: "aaa \"인덱스 (.NET API-Azure 검색) | \"Microsoft Docs"
description: "Hello Azure 검색.NET SDK를 사용 하 여 코드에서 인덱스를 만듭니다."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 3a851647-fc7b-4fb6-8506-6aaa519e77cd
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 7fa4030b8c3565bc02b1d6bb4426331657cf3a5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-net-sdk"></a>Hello.NET SDK를 사용 하 여 Azure 검색 인덱스 만들기
> [!div class="op_single_selector"]
> * [개요](search-what-is-an-index.md)
> * [포털](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST (영문)](search-create-index-rest-api.md)
> 
> 

이 문서에서는 Azure 검색을 만드는 hello 과정 안내 합니다 [인덱스](https://docs.microsoft.com/rest/api/searchservice/Create-Index) hello를 사용 하 여 [Azure 검색.NET SDK](https://aka.ms/search-sdk)합니다.

이 가이드를 수행하고 인덱스를 만들기 전에 이미 [Azure 검색 서비스를 만들어야](search-create-service-portal.md)합니다.

> [!NOTE]
> 이 문서의 모든 샘플 코드는 C#으로 작성되었습니다. Hello 전체 소스 코드를 찾을 수 [GitHub에서](http://aka.ms/search-dotnet-howto)합니다. Hello에 대 한 읽을 수 있습니다 [Azure 검색.NET SDK](search-howto-dotnet-sdk.md) hello 샘플 코드의 자세한 연습 과정에 대 한 합니다.


## <a name="identify-your-azure-search-services-admin-api-key"></a>Azure 검색 서비스의 관리 API 키 식별
Azure 검색 서비스를 프로 비전 했으므로 hello.NET SDK를 사용 하 여 서비스 끝점에 대해 거의 준비 되었습니다 tooissue 요청 됩니다. 첫째, 키 중 하나가 hello 관리 api-생성 된 tooobtain hello 검색 서비스를 프로 비전 할 필요 합니다. hello.NET SDK는 모든 요청 tooyour 서비스에서이 api 키를 전송 합니다. 유효한 키가 있는 hello 요청 보내기 hello 응용 프로그램 사이이 처리 하는 hello 서비스 요청 별로 신뢰를 설정 합니다.

1. toofind toohello 로그인 서비스의 api 키 [Azure 포털](https://portal.azure.com/)
2. Tooyour Azure 검색 서비스 블레이드로 이동
3. Hello에 "키" 아이콘을 클릭

서비스에는 *관리 키* 및 *쿼리 키*가 있습니다.

* 기본 및 보조 *관리자 키는* hello 기능 toomanage hello 서비스 등 tooall 작업 대 한 모든 권한 부여를 만들고 인덱스, 인덱서 및 데이터 원본을 삭제 합니다. 두 가지 tooregenerate hello 기본 키, 그 반대의 경우 toouse hello에 대 한 보조 키를 계속할 수 있도록 합니다.
* 프로그램 *키 쿼리* tooindexes 읽기 전용 액세스 및 문서를 부여 하 고 일반적으로 분산된 tooclient 하는 응용 프로그램이 검색 요청을 실행 합니다.

인덱스 만들기의 hello 용도로 사용할 수 있습니다 프로그램 주 또는 보조 관리자 키입니다.

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-hello-searchserviceclient-class"></a>Hello SearchServiceClient 클래스의 인스턴스를 만들으십시오
Azure 검색.NET SDK hello toostart를 사용 하 여, toocreate hello 인스턴스의 해야 `SearchServiceClient` 클래스입니다. 이 클래스에는 몇 가지 생성자가 있습니다. 원하는 hello에서는 검색 서비스 이름 및 `SearchCredentials` 매개 변수로 개체입니다. `SearchCredentials` 는 API 키를 래핑합니다.

아래 hello 코드에서는 새 `SearchServiceClient` hello 검색 서비스 이름 및 hello 응용 프로그램 구성 파일에 저장 되어 있는 api 키에 대 한 값을 사용 하 여 (`appsettings.json` hello hello 경우에서 [샘플 응용 프로그램](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

`SearchServiceClient`에는 `Indexes` 속성이 있습니다. 이 속성 toocreate, 목록, 업데이트 하거나 여러 Azure 검색 인덱스를 삭제할 모든 hello 메서드를 제공 합니다.

> [!NOTE]
> hello `SearchServiceClient` 클래스 연결 tooyour 검색 서비스를 관리 합니다. 에 너무 많은 연결을 여는 주문 tooavoid을 시도해 보십시오 tooshare의 단일 인스턴스 `SearchServiceClient` 가능 하면 응용 프로그램에 있습니다. 해당 메서드는 스레드로부터 안전한 tooenable 이러한 공유 합니다.
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a>Azure Search 인덱스를 정의합니다.
단일 호출 toohello `Indexes.Create` 메서드 여 인덱스가 생성 됩니다. 이 메서드는 Azure Search 인덱스를 정의하는 `Index` 개체를 매개 변수로 사용합니다. Toocreate 필요는 `Index` 개체를 다음과 같이 초기화:

1. 집합 hello `Name` hello 속성 `Index` 인덱스 개체 toohello 이름입니다.
2. 집합 hello `Fields` hello 속성 `Index` 개체 tooan 배열을 `Field` 개체입니다. hello 가장 쉬운 방법은 toocreate hello `Field` hello 호출 된 경우 개체 `FieldBuilder.BuildForType` 메서드, 형식 매개 변수 hello에 대 한 모델 클래스를 전달 합니다. 모델 클래스에 인덱스 toohello 필드 매핑 속성이 있습니다. 이렇게 하면 모델 클래스의 사용자 검색 인덱스 tooinstances에서 toobind 문서 있습니다.

> [!NOTE]
> 인덱스를 만들어 여전히 정의할 수 toouse 모델 클래스를 사용 하지 않으려는 경우 `Field` 개체를 직접 합니다. Hello 데이터 형식 (또는 문자열 필드에 대 한 분석기)와 함께 hello 필드 toohello 생성자의 hello 이름을 제공할 수 있습니다. `IsSearchable`, `IsFilterable` 등의 기타 속성을 설정할 수도 있습니다.
>
>

각 필드 hello를 할당 해야 하는 대로 인덱스를 디자인할 때 염두에 검색 사용자 환경과 비즈니스 요구 유지 한다는 것 [속성을 적절 한](https://docs.microsoft.com/rest/api/searchservice/Create-Index)합니다. 검색 기능 (필터링, 패싯, 정렬 등 전체 텍스트 검색) 되는 이러한 속성 제어 toowhich 필드를 적용 합니다. 명시적으로 설정 하지 않으면 모든 속성에 대 한 hello `Field` 특별히 설정 하지 않으면 toodisabling hello 해당 검색 기능 클래스의 기본값입니다.

예를 들어 인덱스 "호텔"의 이름을 지정하고 모델 클래스를 사용해 필드를 정의했습니다. Hello 모델 클래스의 각 속성에 hello hello 해당 인덱스 필드의 데이터 검색 관련 동작을 결정 하는 특성이 있습니다. hello 모델 클래스는 다음과 같이 정의 됩니다.

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

어떻게 생각 응용 프로그램에서 사용 됩니다에 따라 각 속성에 대 한 hello 특성 선택한 신중 하 게 합니다. 예를 들어 호텔에 대 한 검색 하는 사용자 수 hello에서 일치 하는 키워드에에서 관심은 `description` hello를 추가 하 여 해당 필드에 대 한 전체 텍스트 검색 설정 되므로 필드 `IsSearchable` toohello 특성 `Description` 속성.

형식의 인덱스에는 정확히 하나의 필드 점에 유의 하십시오 `string` hello로 지정 해야 hello *키* hello를 추가 하 여 필드 `Key` 특성 (참조 `HotelId` 위 예제는 hello에).

위의 hello 인덱스 정의 언어 분석기를 사용 하 여 hello에 대 한 `description_fr` 것은 의도 한 toostore 프랑스어 텍스트 필드입니다. 참조 [hello 언어 지원 항목](https://docs.microsoft.com/rest/api/searchservice/Language-support) hello 해당 뿐만 아니라 [블로그 게시물](https://azure.microsoft.com/blog/language-support-in-azure-search/) 언어 분석기에 대 한 자세한 내용은 합니다.

> [!NOTE]
> 기본적으로 모델 클래스의 각 속성의 hello 이름 hello hello 인덱스의 해당 필드의 hello 이름으로 사용 됩니다. 모든 속성 이름이 toocamel 경우 필드 이름을 toomap을 원하는 경우 표시할 hello 사용 하 여 hello 클래스 `SerializePropertyNamesAsCamelCase` 특성입니다. Toomap tooa 다른 이름을 경우 hello를 사용할 수 있습니다 `JsonProperty` hello와 같은 특성 `DescriptionFr` 위의 속성입니다. hello `JsonProperty` 특성 우선 순위가 hello `SerializePropertyNamesAsCamelCase` 특성입니다.
> 
> 

모델 클래스를 정의했으므로 인덱스 정의를 아주 쉽게 만들 수 있습니다.

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-hello-index"></a>Hello 인덱스 만들기
초기화 된 했으므로 `Index` 개체를 호출 하 여 hello 인덱스를 만들 수 있습니다 `Indexes.Create` 에 프로그램 `SearchServiceClient` 개체:

```csharp
serviceClient.Indexes.Create(definition);
```

성공적인 요청에 대 한 hello 메서드는 정상적으로 반환 됩니다. 잘못 된 매개 변수 같은 hello 요청에 문제가 있으면 hello 메서드는 throw `CloudException`합니다.

완료 되 면 인덱스 및 원하는 toodelete와 것만 hello 호출 `Indexes.Delete` 메서드를 프로그램 `SearchServiceClient`합니다. 예를 들어 다음은 hello "호텔" 인덱스 삭제는 방법입니다.

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> hello 예제 코드에서는이 문서에 간단한 설명을 위해 hello Azure 검색.NET SDK의 hello 동기 메서드를 사용합니다. 사용자 고유의 응용 프로그램 tookeep에 hello 비동기 메서드를 사용 하는 것이 좋습니다 확장성과 응답성이 해당 합니다. 예를 들어 hello 위의 예에서는 사용 하 여 `CreateAsync` 및 `DeleteAsync` 대신 `Create` 및 `Delete`합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
Azure 검색 인덱스를 만든 후 준비가 끝납니다 너무[hello 인덱스에 콘텐츠를 업로드](search-what-is-data-import.md) 데이터 검색을 시작할 수 있도록 합니다.


---
title: "Azure Cosmos DB에서 지리 공간 데이터와 함께 aaaWorking | Microsoft Docs"
description: "어떻게 toocreate, 인덱스 및 Azure Cosmos DB를 사용 하 여 공간 개체를 쿼리하고 DocumentDB API hello 이해 합니다."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a>Azure Cosmos DB에서 지리 공간 및 GeoJSON 위치 데이터 작업
이 문서는 소개 toohello 지리 공간 기능에 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)합니다. 이 읽은 후 다음 질문 수 tooanswer hello 수 있습니다.

* Azure Cosmos DB에 공간 데이터를 저장하려면 어떻게 해야 하나요?
* SQL 및 LINQ에서 Azure Cosmos DB의 지리 공간 데이터를 쿼리하려면 어떻게 해야 하나요?
* Azure Cosmos DB에서 공간 인덱싱을 사용하거나 사용하지 않도록 설정하려면 어떻게 해야 하나요?

이 문서에서는 공간 데이터와 함께 toowork DocumentDB API hello 하는 방법을 보여 줍니다. 코드 샘플은 이 [GitHub 프로젝트](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs)를 참조하세요.

## <a name="introduction-toospatial-data"></a>Toospatial 데이터 소개
Hello 위치와 모양 공간에서 개체의 공간 데이터에 설명합니다. 대부분의 응용 프로그램에서 이러한 tooobjects hello 지구, 즉, 지리 공간적 데이터에 해당합니다. 공간 데이터는 사용자의 사용된 toorepresent hello 위치, 도시 또는 호수 hello 경계 또는 관심 있는 전체 가능 합니다. 일반적인 사용 사례에는 종종 근접 쿼리(예: "내 현재 위치 근처의 모든 커피숍 찾기")가 포함됩니다. 

### <a name="geojson"></a>GeoJSON
인덱싱 및 쿼리 hello를 사용 하 여 표현 되는 지리 공간 지점 데이터의 azure Cosmos DB 지원 [GeoJSON 사양](https://tools.ietf.org/html/rfc7946)합니다. GeoJSON 데이터 구조는 항상 유효한 JSON 개체이므로 특수 도구나 라이브러리 없이 Azure Cosmos DB를 사용하여 저장 및 쿼리할 수 있습니다. hello Azure Cosmos DB Sdk 도우미 클래스와 쉽게 toowork 공간 데이터와 함께 구성 하는 메서드를 제공 합니다. 

### <a name="points-linestrings-and-polygons"></a>Points, LineStrings 및 Polygons
**점** 은 공간 내의 단일 위치를 나타냅니다. 지리 공간 데이터는 지점 식품점, 키오스크, 자동차 또는 도시의 실제 주소 될 수 있는 hello 정확한 위치를 나타냅니다.  점은 좌표 쌍이나 경도 및 위도를 사용하여 GeoJSON(및 Azure Cosmos DB)에서 표시됩니다. 점에 대한 예제 JSON은 다음과 같습니다.

**Azure Cosmos DB의 점**

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> hello GeoJSON 사양 경도 지정 하 고 첫 번째 위도 두 번째입니다. 다른 매핑 응용 프로그램과 마찬가지로 경도와 위도는 각도이며 도 단위로 표시됩니다. 경도 값 hello 본초 자오선에서에서 측정 되 고-180 180.0도 및 위도 사이 값 hello 적도에서 측정 되 고-90.0 사이 90.0도 합니다. 
> 
> Azure Cosmos DB 당 hello WGS 84 참조 시스템에 표시 된 대로 좌표를 해석 합니다. 좌표 참조 시스템에 대한 자세한 내용은 아래를 참조하세요.
> 
> 

위치 데이터를 포함하는 이 사용자 프로필 예제와 같이 Azure Cosmos DB 문서에 포함할 수 있습니다.

**위치가 Azure Cosmos DB에 저장되어 있는 프로필 사용**

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

또한 toopoints, GeoJSON LineStrings 다각형과 지원합니다. **LineStrings** 을 연결 하는 선 세그먼트 hello 및에 두 개 이상의 점 계열을 나타냅니다. 지리 공간적 데이터 LineStrings은 자주 사용 되는 toorepresent 고속도 또는 강 합니다. **Polygon**은 닫힌 LineString을 형성하는 연결된 점의 경계입니다. 다각형은 자주 사용 되는 toorepresent 호수와 같은 자연 대형 또는 도시 및 상태와 같은 정치적 관할지입니다. Azure Cosmos DB에서 다각형의 예는 다음과 같습니다. 

**GeoJSON의 다각형**

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> hello GeoJSON 유효한 다각형에 대 한 hello 마지막 좌표 쌍을 제공 해야 함을 필요을 hello hello 첫 번째 toocreate 폐쇄형된 도형으로 동일 합니다.
> 
> 다각형 내의 점을 시계 반대 방향 순서로 지정해야 합니다. 시계 방향으로 순서에 지정 된 다각형 hello hello 영역 내에서 역을 수를 나타냅니다.
> 
> 

LineString 및 다각형, 더하기 tooPoint GeoJSON도 지정 방법에 대 한 hello 표현 toogroup는 방법과 여러 지리 공간 위치도 지리적 위치를 사용 하 여 임의의 속성 tooassociate는 **기능**합니다. 이러한 개체는 유효한 JSON이므로 모두 Azure Cosmos DB에 저장하고 처리할 수 있습니다. 그러나 Azure Cosmos DB는 지점의 자동 인덱싱만 지원합니다.

### <a name="coordinate-reference-systems"></a>좌표 참조 시스템
Hello 지구 hello 모양 일반 이므로 지리 공간 데이터의 좌표 각각 프레임을 참조 및 측정 단위 많은 좌표 참조 시스템 (CR)으로 표시 됩니다. 예를 들어 "Britain National 그리드" hello 참조 시스템은 매우 정확 하 게는 외부가 아니라 hello United Kingdom에 대 한 합니다. 

hello 사용에서 가장 인기 있는 CRS 오늘는 hello World Geodetic System [WGS 84](http://earth-info.nga.mil/GandG/wgs84/)합니다. GPS 장치와 Google Map 및 Bing 지도 API를 비롯한 많은 매핑 서비스는 WGS-84를 사용합니다. Azure Cosmos DB 인덱싱 및 WGS 84 CRS hello를 사용 하 여 지리 공간 데이터 쿼리를 지원 합니다. 

## <a name="creating-documents-with-spatial-data"></a>공간 데이터를 포함하는 문서 만들기
GeoJSON 값이 포함 된 문서를 만들 때 자동으로 hello 컬렉션의 toohello 인덱싱 정책에 따라에 공간 인덱스와 인덱스 됩니다. Python 또는 Node.js와 같은 동적으로 형식화된 언어로 Azure Cosmos DB SDK 작업을 수행하는 경우 유효한 GeoJSON을 만들어야 합니다.

**Node.js에서 지리 공간 데이터를 포함하는 문서 만들기**

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

Hello hello DocumentDB Api를 사용 하는 경우 사용할 수 있습니다 `Point` 및 `Polygon` hello 내의 클래스 `Microsoft.Azure.Documents.Spatial` 응용 프로그램 개체 내에서 네임 스페이스 tooembed 위치 정보입니다. 이러한 클래스 간소화할 hello serialization 및 deserialization 공간 데이터의 GeoJSON에 있습니다.

**.NET에서 지리 공간 데이터를 포함하는 문서 만들기**

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

Hello 위도 및 경도 정보 없는 해도 hello 실제 주소 또는 위치 이름 국가 또는 도시와 같은 경우 Bing 지도 REST 서비스와 같은 지 오 코딩 서비스를 사용 하 여 hello 실제 좌표를 조회할 수 있습니다. [여기](https://msdn.microsoft.com/library/ff701713.aspx)서 Bing 지도 지오코딩에 대해 자세히 알아보세요.

## <a name="querying-spatial-types"></a>공간 형식 쿼리
이전 지나온 어떻게 했으므로 tooinsert 지리 공간 데이터는 방법에 살펴보겠습니다 tooquery SQL 및 LINQ를 사용 하 여 Azure Cosmos DB를 사용 하 여이 데이터입니다.

### <a name="spatial-sql-built-in-functions"></a>공간 SQL 기본 제공 함수
Azure Cosmos DB hello Open Geospatial Consortium (OGC) 기본 제공 함수를 쿼리 하는 지리 공간에 대 한 다음을 지원 합니다. Hello 전체 집합의 기본 제공 함수 hello SQL 언어에에서 대 한 자세한 내용은 참조 하십시오 너무[쿼리 Azure Cosmos DB](documentdb-sql-query.md)합니다.

<table>
<tr>
  <td><strong>사용 현황</strong></td>
  <td><strong>설명</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE(spatial_expr, spatial_expr)</td>
  <td>두 hello GeoJSON 지점, 다각형 또는 LineString 식 사이의 hello 거리를 반환합니다.</td>
</tr>
<tr>
  <td>ST_WITHIN(spatial_expr, spatial_expr)</td>
  <td>Hello 첫 번째 GeoJSON 개체 (점, 다각형, 또는 LineString) hello 두 번째 GeoJSON 개체 (점, 다각형, 또는 LineString) 이내 인지 여부를 나타내는 부울 식을 반환 합니다.</td>
</tr>
<tr>
  <td>ST_INTERSECTS(spatial_expr, spatial_expr)</td>
  <td>Hello 지정 된 두 GeoJSON 개체 (점, 다각형, 또는 LineString) 교차 하는지 여부를 나타내는 부울 식을 반환 합니다.</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Hello GeoJSON 지점, 다각형 또는 LineString 식이 유효한 경우이 지정 되었는지 여부를 나타내는 부울 값을 반환 합니다.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Hello GeoJSON 지점, 다각형 또는 LineString 식이 지정 된 경우 부울 값을 포함 하는 JSON 값은 유효 하 고, 잘못 된 경우에 문자열 값으로 이유 hello 또한 반환 합니다.</td>
</tr>
</table>

공간 함수에는 공간 데이터에 대 한 사용된 tooperform 근접 쿼리 수 있습니다. 예를 들어 여기에 모든 제품군에 설명 하의 hello 30 km 내에서 지정 된 위치 사용 하는 hello ST_DISTANCE 기본 제공 함수를 반환 하는 쿼리입니다. 

**쿼리**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**결과**

    [{
      "id": "WakefieldFamily"
    }]

공간 인덱싱 인덱싱 정책에 포함 하는 경우 다음 "거리 쿼리"는 제공 효율적으로 hello 인덱스를 통해. 공간 인덱싱에 대 한 자세한 내용은 아래의 hello 섹션을 참조 하십시오. Spatial 없는 경우 경로 지정 하는 hello에 대 한 인덱스, 공간 쿼리를 지정 하 여 수행할 수 있습니다 `x-ms-documentdb-query-enable-scan` hello 값을 가진 요청 헤더가 너무 "true"로 설정 합니다. .NET에서는 이렇게 하 여 선택적 전달 hello **FeedOptions** 와 인수 tooqueries [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) tootrue를 설정 합니다. 

ST_WITHIN 점이 다각형 내에서 사용 되는 toocheck 될 수 있습니다. 일반적으로 다각형은 우편 번호, 상태 경계 또는 자연 형성 되어 작업이 사용 되는 toorepresent 경계입니다. 다시 인덱싱 정책에 공간 인덱싱에 포함 하면 다음 "내의" 쿼리는 제공 효율적으로 hello 인덱스를 통해. 

다각형 인수 ST_WITHIN에 단일 링만 포함 될 수 있습니다, 그리고 즉, hello 다각형의 구멍 포함 되지 않아야 합니다. 

**쿼리**

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

**결과**

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> 형식이 잘못 되었거나, 잘못 된 인수는 다음 것 너무 평가 중 하나에 지정 된 hello 위치 값 하는 경우 Azure Cosmos DB 쿼리에서 작동 하는 비슷한 toohow 일치 하지 않는 형식이**정의 되지 않은** 평가 hello 문서 toobe hello에서 생략 쿼리 결과입니다. 쿼리 결과가 없으면 ST_ISVALIDDETAILED toodebug hello spatail 형식이 유효 하지 않은 이유를 실행 합니다.     
> 
> 

Azure Cosmos DB도 역 쿼리 수행을 지원, 다각형 또는 Azure Cosmos DB에 있는 줄 인덱스 다음 지정된 된 위치를 포함 하는 hello 영역에 대 한 쿼리, 즉 있습니다. 이 패턴은 물류 tooidentify에 일반적으로 사용 됩니다. 예를 들어 때 트럭 모드로 들어가거나 나올 지정된 된 영역입니다. 

**쿼리**

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


**결과**

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

ST_ISVALID 및 ST_ISVALIDDETAILED 공간 개체가 유효한 경우 사용 되는 toocheck 수 있습니다. 예를 들어 다음 쿼리에서 hello 범위 위도 값 (-132.8) 부족 한 지점의 hello 유효성을 검사 합니다. 부울 및 이유는 것이 잘못 된 hello 이유를 포함 하는 문자열 ST_ISVALIDDETAILED 반환 hello 가져오고 ST_ISVALID 부울 값을 반환 합니다.

** 쿼리 **

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

**결과**

    [{
      "$1": false
    }]

이러한 함수에 사용 되는 toovalidate 다각형 될 수도 있습니다. 예를 들어 여기 사용 ST_ISVALIDDETAILED toovalidate 닫히지 않은 다각형 합니다. 

**쿼리**

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

**결과**

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a>Hello.NET SDK에서에서 LINQ 쿼리
DocumentDB.NET SDK hello 공급자 메서드를 스텁도 `Distance()` 및 `Within()` LINQ 식에서 사용할 수 있도록 합니다. hello DocumentDB LINQ 공급자 호출으로 변환 이러한 메서드 호출 toohello 동등한 SQL 기본 제공 함수 (ST_DISTANCE 및 ST_WITHIN 각각). 

여기의 hello Azure Cosmos DB "위치" 값은 30 km hello의의 반지름 내에서 지정 된 컬렉션에서 모든 문서를 찾습니다. LINQ 쿼리의 예제 LINQ를 사용 하 여 가리킵니다.

**거리에 대한 LINQ 쿼리**

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

마찬가지로, 여기에 해당 "위치" hello 내는 모든 hello 문서 상자/다각형 지정을 찾기 위한 쿼리입니다. 

**이내에 대한 LINQ 쿼리**

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


이전 지나온 어떻게 했으므로 tooquery 문서 LINQ과 SQL을 사용 하는 방법에 살펴보겠습니다 tooconfigure Azure Cosmos DB 공간 인덱싱에 대 한 합니다.

## <a name="indexing"></a>인덱싱
Hello에서 설명 했 듯이 [Azure Cosmos DB를 사용 하 여 스키마를 알 수 없는 인덱싱](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) 용지으로 설계 했으므로 Azure Cosmos DB 데이터베이스 엔진 toobe 진정으로 스키마를 알 수 없는 JSON에 대 한 최고 수준의 지원도 제공 합니다. 기본적으로 Azure Cosmos DB의 hello 쓰기 액세스에 최적화 된 데이터베이스 엔진 hello GeoJSON 표준에 표시 된 공간 데이터 (가리킴, 다각형 및 선)을 이해 합니다.

간단히 말해서 hello 기 하 도형이 측 지 좌표를 2D 평면에에서 예상 하는 경우 사용 하 여 셀을 점진적으로 나뉩니다는 **quadtree**합니다. 이러한 셀은 hello 셀 내에서 hello 위치에 따라 매핑된 too1D는 **힐베르트 공간 채움 곡선**, 지점의 위치를 유지 합니다. 또한 위치 데이터가 인덱싱될 때 프로세스를 거치는 라고 **공간 분할**, 즉, 모든 hello 셀 위치와 교차 하는 식별 되 고 hello Azure Cosmos DB 인덱스의 키로 저장 합니다. 쿼리 시 점 및 다각형은 또한 없을된 tooextract 처럼 인수 관련 셀 ID 범위 hello 다음 tooretrieve 데이터 hello 인덱스를 사용 합니다.

에 대 한 공간 인덱스를 포함 하는 인덱싱 정책이 지정 하는 경우 / * (모든 경로), 다음 hello 컬렉션 내에 있는 모든 지점 (ST_WITHIN 및 ST_DISTANCE) 효율적인 공간 쿼리를 위해 인덱싱됩니다. 공간 인덱스에는 전체 자릿수 값이 없으며 항상 기본 전체 자릿수 값을 사용합니다.

> [!NOTE]
> Azure Cosmos DB는 점, 다각형 및 LineStrings의 자동 인덱싱을 지원합니다.
> 
> 

hello 다음 JSON 코드 조각은 인덱싱 정책을 공간 인덱싱을 사용할 수 있는, 즉, 인덱스를 쿼리 하는 공간에 대 한 문서 내에 있는 모든 GeoJSON 지점. 인덱싱 정책을 hello Azure 포털을 사용 하 여 hello를 수정 하는 경우 JSON 정책 tooenable 컬렉션에 인덱스가 공간 인덱싱에 따라 hello를 지정할 수 있습니다.

**점 및 다각형에 대한 공간 인덱싱이 사용되는 컬렉션 인덱싱 정책 JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

다음은 toocreate 공간 인덱싱 사용 하 여 컬렉션에 점을 포함 하는 모든 경로 대해 설정 하는 방법을 보여 주는.net 코드 조각입니다. 

**공간 인덱싱을 사용하여 컬렉션 만들기**

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

및 문서 내에 저장 된 모든 지점을 통한 공간 인덱싱의 기존 컬렉션 tootake 장점은 수정 하는 방법을 다음과 같습니다.

**공간 인덱싱을 사용하여 기존 컬렉션 수정**

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> Hello 위치 hello 문서 내에서 GeoJSON 값 형식이 잘못 되었거나 잘못 된 경우 다음 것은 가져올 인덱싱되지 공간 쿼리. ST_ISVALID 및 ST_ISVALIDDETAILED를 사용하여 위치 값의 유효성을 검사할 수 있습니다.
> 
> 컬렉션 정의가 파티션 키를 포함하는 경우 인덱싱 변환 진행률은 보고되지 않습니다. 
> 
> 

## <a name="next-steps"></a>다음 단계
익힌 한 했으므로 Azure Cosmos DB의 지리 공간 지원과 함께 tooget 시작 방법에 대 한 할 수 있습니다.

* Hello를 사용 하 여 코딩 시작 [GitHub의 지리 공간.NET 코드 샘플](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)
* 받기 hello에 쿼리 하는 지리 공간으로 [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)
* [Azure Cosmos DB 쿼리](documentdb-sql-query.md)에 대해 알아보기
* [Azure Cosmos DB 인덱싱 정책에 대해 알아보기](indexing-policies.md)


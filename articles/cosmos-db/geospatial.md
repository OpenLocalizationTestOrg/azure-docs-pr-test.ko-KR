---
title: "Azure Cosmos DB에서 지리 공간 데이터 작업 | Microsoft Docs"
description: "Azure Cosmos DB 및 DocumentDB API를 사용하여 공간 개체를 만들고 인덱싱 및 쿼리하는 방법을 이해합니다."
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
ms.openlocfilehash: d5785c81fb597e7d30eb7d3a880e7194d8358ed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="d883b-103">Azure Cosmos DB에서 지리 공간 및 GeoJSON 위치 데이터 작업</span><span class="sxs-lookup"><span data-stu-id="d883b-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="d883b-104">이 문서에서는 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)의 지리 공간 기능을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="d883b-105">이 문서를 읽은 후에는 다음과 같은 질문에 답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="d883b-106">Azure Cosmos DB에 공간 데이터를 저장하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d883b-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="d883b-107">SQL 및 LINQ에서 Azure Cosmos DB의 지리 공간 데이터를 쿼리하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d883b-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="d883b-108">Azure Cosmos DB에서 공간 인덱싱을 사용하거나 사용하지 않도록 설정하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d883b-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="d883b-109">이 문서에는 DocumentDB API를 통해 공간 데이터를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-109">This article shows how to work with spatial data with the DocumentDB API.</span></span> <span data-ttu-id="d883b-110">코드 샘플은 이 [GitHub 프로젝트](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d883b-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="d883b-111">공간 데이터 소개</span><span class="sxs-lookup"><span data-stu-id="d883b-111">Introduction to spatial data</span></span>
<span data-ttu-id="d883b-112">공간 데이터는 공간에서 개체의 위치와 모양을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-112">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="d883b-113">대부분의 응용 프로그램에서 이러한 데이터는 지구의 개체, 즉 지리 공간 데이터에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-113">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span></span> <span data-ttu-id="d883b-114">공간 데이터를 사용하여 사람, 관심 있는 장소 또는 도시나 호수 경계의 위치를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="d883b-115">일반적인 사용 사례에는 종종 근접 쿼리(예: "내 현재 위치 근처의 모든 커피숍 찾기")가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="d883b-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="d883b-116">GeoJSON</span></span>
<span data-ttu-id="d883b-117">Azure Cosmos DB는 인덱싱 및 지리 공간 지점 데이터의 쿼리를 지원하고 [GeoJSON 사양](https://tools.ietf.org/html/rfc7946)을 사용하여 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="d883b-118">GeoJSON 데이터 구조는 항상 유효한 JSON 개체이므로 특수 도구나 라이브러리 없이 Azure Cosmos DB를 사용하여 저장 및 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="d883b-119">Azure Cosmos DB SDK는 쉽게 공간 데이터로 작업할 수 있게 해주는 도우미 클래스와 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="d883b-120">Points, LineStrings 및 Polygons</span><span class="sxs-lookup"><span data-stu-id="d883b-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="d883b-121">**점** 은 공간 내의 단일 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="d883b-122">지리 공간 데이터에서 점은 식품점, 키오스크, 자동차 또는 도시의 주소일 수 있는 정확한 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="d883b-123">점은 좌표 쌍이나 경도 및 위도를 사용하여 GeoJSON(및 Azure Cosmos DB)에서 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="d883b-124">점에 대한 예제 JSON은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="d883b-125">**Azure Cosmos DB의 점**</span><span class="sxs-lookup"><span data-stu-id="d883b-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="d883b-126">GeoJSON 사양은 경도를 먼저 지정하고 위도를 두 번째로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-126">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="d883b-127">다른 매핑 응용 프로그램과 마찬가지로 경도와 위도는 각도이며 도 단위로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="d883b-128">경도 값은 본초 자오선에서 측정되고 -180도와 180.0도 사이이고, 위도 값은 적도에서 측정되고 -90.0도와 90.0도 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-128">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="d883b-129">Azure Cosmos DB는 WGS-84 참조 시스템을 기준으로 좌표를 해석합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="d883b-130">좌표 참조 시스템에 대한 자세한 내용은 아래를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d883b-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="d883b-131">위치 데이터를 포함하는 이 사용자 프로필 예제와 같이 Azure Cosmos DB 문서에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="d883b-132">**위치가 Azure Cosmos DB에 저장되어 있는 프로필 사용**</span><span class="sxs-lookup"><span data-stu-id="d883b-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="d883b-133">점 외에도 GeoJSON은 LineString 및 다각형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="d883b-134">**LineString** 은 공간의 둘 이상 점과 이러한 점을 연결하는 선 세그먼트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="d883b-135">지리 공간 데이터에서 LineStrings은 일반적으로 고속도로나 강을 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="d883b-136">**Polygon**은 닫힌 LineString을 형성하는 연결된 점의 경계입니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="d883b-137">다각형은 일반적으로 호수와 같은 자연스러운 대형이나 구/군/시 및 시/도와 같은 정치적 관할지를 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="d883b-138">Azure Cosmos DB에서 다각형의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="d883b-139">**GeoJSON의 다각형**</span><span class="sxs-lookup"><span data-stu-id="d883b-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="d883b-140">GeoJSON 사양에서는 유효한 다각형이 되기 위해 마지막 좌표 쌍을 첫 번째 좌표 쌍과 동일하게 제공하여 닫힌 도형을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="d883b-141">다각형 내의 점을 시계 반대 방향 순서로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="d883b-142">시계 방향 순서로 지정된 다각형은 내부 영역의 반전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="d883b-143">점, LineString 및 다각형 외에도 GeoJSON은 여러 지리 공간 위치를 그룹화하는 방법 및 임의 속성을 지리적 위치에 **기능**으로 연결하는 방법에 대한 표현을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-143">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="d883b-144">이러한 개체는 유효한 JSON이므로 모두 Azure Cosmos DB에 저장하고 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="d883b-145">그러나 Azure Cosmos DB는 지점의 자동 인덱싱만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="d883b-146">좌표 참조 시스템</span><span class="sxs-lookup"><span data-stu-id="d883b-146">Coordinate reference systems</span></span>
<span data-ttu-id="d883b-147">지구 모양이 불규칙적이므로 지리 공간 데이터의 좌표는 각각 고유한 참조 프레임과 측정 단위가 있는 많은 CRS(좌표 참조 시스템)에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-147">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="d883b-148">예를 들어 "National Grid of Britain"은 영국에서만 매우 정확하고 그 밖의 지역에서는 정확하지 않은 참조 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-148">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="d883b-149">현재 가장 많이 사용되는 CRS는 World Geodetic System [WGS-84](http://earth-info.nga.mil/GandG/wgs84/)입니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="d883b-150">GPS 장치와 Google Map 및 Bing 지도 API를 비롯한 많은 매핑 서비스는 WGS-84를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="d883b-151">Azure Cosmos DB는 WGS-84 CRS만 사용하여 지리 공간 데이터의 인덱싱 및 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="d883b-152">공간 데이터를 포함하는 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="d883b-152">Creating documents with spatial data</span></span>
<span data-ttu-id="d883b-153">GeoJSON 값을 포함하는 문서를 만드는 경우 컬렉션의 인덱싱 정책에 따라 공간 인덱스를 사용하여 자동으로 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span></span> <span data-ttu-id="d883b-154">Python 또는 Node.js와 같은 동적으로 형식화된 언어로 Azure Cosmos DB SDK 작업을 수행하는 경우 유효한 GeoJSON을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="d883b-155">**Node.js에서 지리 공간 데이터를 포함하는 문서 만들기**</span><span class="sxs-lookup"><span data-stu-id="d883b-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within the callback
});
```

<span data-ttu-id="d883b-156">DocumentDB API로 작업하는 경우 `Microsoft.Azure.Documents.Spatial` 네임스페이스 내에서 `Point` 및 `Polygon` 클래스를 사용하여 위치 정보를 응용 프로그램 개체 내에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-156">If you're working with the DocumentDB APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span></span> <span data-ttu-id="d883b-157">이러한 클래스는 GeoJSON으로 공간 데이터 직렬화 및 역직렬화를 간소화하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="d883b-158">**.NET에서 지리 공간 데이터를 포함하는 문서 만들기**</span><span class="sxs-lookup"><span data-stu-id="d883b-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="d883b-159">위도 및 경도 정보가 없지만 실제 주소나 도시 또는 국가와 같은 위치 이름이 있는 경우 Bing 지도 REST 서비스와 같은 지오코딩 서비스를 사용하여 실제 좌표를 조회할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="d883b-160">[여기](https://msdn.microsoft.com/library/ff701713.aspx)서 Bing 지도 지오코딩에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d883b-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="d883b-161">공간 형식 쿼리</span><span class="sxs-lookup"><span data-stu-id="d883b-161">Querying spatial types</span></span>
<span data-ttu-id="d883b-162">지리 공간 데이터를 삽입하는 방법을 살펴보았으며, 이제 SQL 및 LINQ에서 Azure Cosmos DB를 사용하여 이 데이터를 쿼리하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="d883b-163">공간 SQL 기본 제공 함수</span><span class="sxs-lookup"><span data-stu-id="d883b-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="d883b-164">Azure Cosmos DB는 지리 공간 쿼리를 위해 다음과 같은 OGC(Open Geospatial Consortium) 기본 제공 함수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="d883b-165">SQL 언어의 전체 기본 제공 함수 집합에 대한 자세한 내용은 [Azure Cosmos DB 쿼리](documentdb-sql-query.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d883b-165">For more details on the complete set of built-in functions in the SQL language, please refer to [Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="d883b-166"><strong>사용 현황</strong></span><span class="sxs-lookup"><span data-stu-id="d883b-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="d883b-167"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="d883b-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d883b-168">ST_DISTANCE(spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="d883b-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="d883b-169">두 GeoJSON Point, Polygon 또는 LineString 식 사이의 거리를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d883b-170">ST_WITHIN(spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="d883b-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="d883b-171">첫 번째 GeoJSON 개체(Point, Polygon 또는 LineString)가 두 번째 GeoJSON 개체(Point, Polygon 또는 LineString) 내에 있는지를 나타내는 부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d883b-172">ST_INTERSECTS(spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="d883b-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="d883b-173">지정한 두 GeoJSON 개체(Point, Polygon 또는 LineString)가 교차하는지 여부를 나타내는 부울 식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d883b-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="d883b-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="d883b-175">지정된 GeoJSON Point, Polygon 또는 LineString 식이 유효한지 여부를 나타내는 부울 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d883b-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="d883b-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="d883b-177">지정된 GeoJSON Point, Polygon 또는 LineString 식이 유효한 경우 부울 값을 포함하는 JSON 값을 반환하고, 잘못된 경우 추가로 그 이유를 문자열 값으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="d883b-178">공간 함수를 사용하여 공간 데이터에 대한 근접 쿼리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-178">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="d883b-179">예를 들어 ST_DISTANCE 기본 제공 함수를 사용하여 지정된 위치에서 30km 이내에 있는 모든 제품군 문서를 반환하는 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="d883b-180">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="d883b-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="d883b-181">**결과**</span><span class="sxs-lookup"><span data-stu-id="d883b-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="d883b-182">인덱싱 정책에 공간 인덱싱을 포함하면 "거리 쿼리"가 인덱스를 통해 효율적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="d883b-183">공간 인덱싱에 대한 자세한 내용은 아래 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d883b-183">For more details on spatial indexing, please see the section below.</span></span> <span data-ttu-id="d883b-184">지정된 경로에 대한 공간 인덱스가 없는 경우에도 값이 "true"로 설정된 `x-ms-documentdb-query-enable-scan` 요청 헤더를 지정하여 공간 쿼리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="d883b-185">.NET에서는 **EnableScanInQuery** 가 true로 설정된 쿼리에 선택적 [FeedOptions](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) 인수를 전달하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="d883b-186">ST_WITHIN을 사용하여 점이 다각형 내에 있는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="d883b-187">일반적으로 다각형은 우편 번호, 시/도 경계 또는 자연스러운 대형과 같은 경계를 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="d883b-188">인덱싱 정책에 공간 인덱싱을 포함하면 "이내" 쿼리가 인덱스를 통해 효율적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="d883b-189">ST_WITHIN의 다각형 인수에는 단일 링만 포함될 수 있습니다. 즉, 다각형에 구멍이 포함되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="d883b-190">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="d883b-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="d883b-191">**결과**</span><span class="sxs-lookup"><span data-stu-id="d883b-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="d883b-192">Azure Cosmos DB 쿼리에서 일치하지 않는 형식이 작동하는 방식과 비슷하게, 인수에 지정된 위치 값이 잘못되었거나 형식이 잘못된 경우 **정의되지 않음** 으로 평가되고 평가된 문서는 쿼리 결과에서 생략됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-192">Similar to how mismatched types works in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="d883b-193">쿼리에서 결과가 반환되지 않는 경우 ST_ISVALIDDETAILED를 실행하여 공간 형식이 잘못된 이유를 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="d883b-194">Azure Cosmos DB는 반전 쿼리 수행도 지원합니다. 즉, Azure Cosmos DB에서 다각형 또는 선을 인덱싱한 다음 지정된 점이 포함된 영역을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="d883b-195">이 패턴은 일반적으로 특정 시점(예: 지정된 영역에 트럭이 출입한 시점)을 식별하기 위해 물류에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-195">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="d883b-196">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="d883b-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="d883b-197">**결과**</span><span class="sxs-lookup"><span data-stu-id="d883b-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="d883b-198">ST_ISVALID 및 ST_ISVALIDDETAILED를 사용하여 공간 개체가 유효한지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="d883b-199">예를 들어 다음 쿼리는 위도 값(-132.8)이 범위를 벗어난 점의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="d883b-200">ST_ISVALID는 부울 값만 반환하고 ST_ISVALIDDETAILED는 부울 및 잘못된 것으로 간주된 이유를 포함하는 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="d883b-201">** 쿼리 **</span><span class="sxs-lookup"><span data-stu-id="d883b-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="d883b-202">**결과**</span><span class="sxs-lookup"><span data-stu-id="d883b-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="d883b-203">이러한 함수를 사용하여 다각형의 유효성을 검사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-203">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="d883b-204">예를 들어 여기서는 ST_ISVALIDDETAILED를 사용하여 닫혀 있지 않은 다각형의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="d883b-205">**쿼리**</span><span class="sxs-lookup"><span data-stu-id="d883b-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="d883b-206">**결과**</span><span class="sxs-lookup"><span data-stu-id="d883b-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="d883b-207">.NET SDK의 LINQ 쿼리</span><span class="sxs-lookup"><span data-stu-id="d883b-207">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="d883b-208">DocumentDB .NET SDK는 LINQ 식에서 사용하기 위한 스텁 메서드 `Distance()` 및 `Within()`도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-208">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="d883b-209">DocumentDB LINQ 공급자는 이러한 메서드 호출을 동등한 SQL 기본 제공 함수 호출(각각 ST_DISTANCE 및 ST_WITHIN)로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-209">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="d883b-210">LINQ를 사용하여 Azure Cosmos DB 컬렉션에서 "위치" 값이 지정된 점에서 30km 반지름 내에 있는 모든 문서를 찾는 LINQ 쿼리의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span></span>

<span data-ttu-id="d883b-211">**거리에 대한 LINQ 쿼리**</span><span class="sxs-lookup"><span data-stu-id="d883b-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="d883b-212">마찬가지로, "위치"가 지정된 상자/다각형 내에 있는 모든 문서를 찾기 위한 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="d883b-213">**이내에 대한 LINQ 쿼리**</span><span class="sxs-lookup"><span data-stu-id="d883b-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="d883b-214">LINQ 및 SQL을 사용하여 문서를 쿼리하는 방법을 살펴보았으며, 이제 공간 인덱싱을 위해 Azure Cosmos DB를 구성하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="d883b-215">인덱싱</span><span class="sxs-lookup"><span data-stu-id="d883b-215">Indexing</span></span>
<span data-ttu-id="d883b-216">[Azure Cosmos DB를 사용한 스키마 제약 없는 인덱싱](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) 에서 설명했듯이 Azure Cosmos DB의 데이터베이스 엔진은 스키마 제약 없이 JSON을 최고 수준으로 지원하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="d883b-217">Azure Cosmos DB의 쓰기 최적화된 데이터베이스 엔진은 GeoJSON 표준으로 표시된 공간 데이터(점, 다각형 및 선)를 기본적으로 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="d883b-218">간단히 말해, 기하 도형이 측지 좌표에서 2D 평면으로 프로젝션된 다음 **quadtree**를 사용하여 셀에 점진적으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="d883b-219">이러한 셀은 점의 위치를 유지하는 **힐버트 공간 채움 곡선** 내의 셀 위치에 따라 1D에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="d883b-220">또한 위치 데이터는 인덱싱될 때 **공간 분할**이라는 프로세스를 거칩니다. 즉, 위치와 교차하는 모든 셀이 식별되고 Azure Cosmos DB 인덱스에 키로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span></span> <span data-ttu-id="d883b-221">쿼리 시 점 및 다각형과 같은 인수도 관련 셀 ID 범위를 추출하기 위해 공간 분할된 다음 인덱스에서 데이터를 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="d883b-222">/*(모든 경로)에 대한 공간 인덱스를 포함하는 인덱싱 정책을 지정하는 경우 효율적인 공간 쿼리(ST_WITHIN 및 ST_DISTANCE)를 위해 컬렉션 내에 있는 모든 점이 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="d883b-223">공간 인덱스에는 전체 자릿수 값이 없으며 항상 기본 전체 자릿수 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="d883b-224">Azure Cosmos DB는 점, 다각형 및 LineStrings의 자동 인덱싱을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="d883b-225">다음 JSON 조각은 공간 인덱싱이 사용되는 인덱싱 정책을 보여 줍니다. 즉, 공간 쿼리를 위해 문서 내에 있는 모든 GeoJSON 점을 인덱싱합니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="d883b-226">Azure 포털을 사용하여 인덱싱 정책을 수정하는 경우 인덱싱 정책에 대해 다음과 같은 JSON을 지정하여 컬렉션에서 공간 인덱싱을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-226">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="d883b-227">**점 및 다각형에 대한 공간 인덱싱이 사용되는 컬렉션 인덱싱 정책 JSON**</span><span class="sxs-lookup"><span data-stu-id="d883b-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="d883b-228">점을 포함하는 모든 경로에 대해 공간 인덱싱이 설정된 컬렉션을 만드는 방법을 보여 주는 .NET 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="d883b-229">**공간 인덱싱을 사용하여 컬렉션 만들기**</span><span class="sxs-lookup"><span data-stu-id="d883b-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="d883b-230">문서 내에 저장된 모든 점에 대해 공간 인덱싱을 활용하도록 기존 컬렉션을 수정하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="d883b-231">**공간 인덱싱을 사용하여 기존 컬렉션 수정**</span><span class="sxs-lookup"><span data-stu-id="d883b-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing to complete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="d883b-232">문서 내의 위치 GeoJSON 값이 잘못되었거나 형식이 잘못된 경우 공간 쿼리를 위해 인덱싱되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="d883b-233">ST_ISVALID 및 ST_ISVALIDDETAILED를 사용하여 위치 값의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="d883b-234">컬렉션 정의가 파티션 키를 포함하는 경우 인덱싱 변환 진행률은 보고되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d883b-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d883b-235">Next steps</span></span>
<span data-ttu-id="d883b-236">Azure Cosmos DB에서 지리 공간 지원을 시작하는 방법을 배웠으므로 이제 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d883b-236">Now that you've learnt about how to get started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="d883b-237">[GitHub의 지리 공간 .NET 코드 샘플](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)을 사용하여 코딩 시작</span><span class="sxs-lookup"><span data-stu-id="d883b-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="d883b-238">[Azure Cosmos DB 쿼리 실습](http://www.documentdb.com/sql/demo#geospatial)에서 지리 공간 쿼리 실습</span><span class="sxs-lookup"><span data-stu-id="d883b-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="d883b-239">[Azure Cosmos DB 쿼리](documentdb-sql-query.md)에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="d883b-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="d883b-240">[Azure Cosmos DB 인덱싱 정책에 대해 알아보기](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="d883b-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>


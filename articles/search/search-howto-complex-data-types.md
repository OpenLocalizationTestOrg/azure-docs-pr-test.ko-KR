---
title: "Azure Search에서 복합 데이터 형식을 모델링하는 방법 | Microsoft Docs"
description: "일반 행 집합 및 컬렉션 데이터 형식을 사용하여 Azure Search 인덱스에서 중첩된 데이터 또는 계층적 데이터 구조를 모델링할 수 있습니다."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: d576fd7bb267ae7a100589413185b595e3b2be42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-model-complex-data-types-in-azure-search"></a><span data-ttu-id="6fd41-103">Azure Search에서 복합 데이터 형식을 모델링하는 방법</span><span class="sxs-lookup"><span data-stu-id="6fd41-103">How to model complex data types in Azure Search</span></span>
<span data-ttu-id="6fd41-104">Azure Search 인덱스를 채우는 데 사용되는 외부 데이터 집합에는 가끔 테이블 형식의 행 집합으로 깔끔하게 분류되지 않는 계층적 또는 중첩된 하위 구조가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-104">External datasets used to populate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="6fd41-105">이러한 구조의 예에는 한 고객에 대한 여러 위치와 전화 번호, 단일 SKU에 대한 여러 색과 크기, 한 권의 책에 대한 여러 저자 등이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="6fd41-106">모델링 용어에서는 이러한 구조를 *복합 데이터 형식*, *복합형 데이터 형식*, *복합성 데이터 형식* 또는 *집계 데이터 형식*이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-106">In modeling terms, you might see these structures referred to as *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, to name a few.</span></span>

<span data-ttu-id="6fd41-107">복합 데이터 형식은 기본적으로 Azure Search에서 지원되지 않지만 입증된 해결책에 구조를 평면화하고 **컬렉션** 데이터 형식을 사용하여 내부 구조를 다시 구성하는 2단계 프로세스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening the structure and then using a **Collection** data type to reconstitute the interior structure.</span></span> <span data-ttu-id="6fd41-108">이 문서에 설명된 기술을 사용하면 콘텐츠를 검색, 패싯, 필터링 및 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-108">Following the technique described in this article allows the content to be searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="6fd41-109">복합 데이터 구조의 예</span><span class="sxs-lookup"><span data-stu-id="6fd41-109">Example of a complex data structure</span></span>
<span data-ttu-id="6fd41-110">일반적으로 이러한 데이터는 JSON 또는 XML 문서 집합으로 또는 Azure Cosmos DB 등의 NoSQL 저장소에 있는 항목으로 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-110">Typically, the data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="6fd41-111">구조적으로, 여러 하위 항목을 검색 및 필터링해야 하므로 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-111">Structurally, the challenge stems from having multiple child items that need to be searched and filtered.</span></span>  <span data-ttu-id="6fd41-112">해결 방법을 설명할 때 일련의 연락처를 예로 나열하는 다음 JSON 문서를 시작점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-112">As a starting point for illustrating the workaround, take the following JSON document that lists a set of contacts as an example:</span></span>

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

<span data-ttu-id="6fd41-113">‘id’, ‘name’ 및 ‘company’라는 이름의 필드를 Azure Search 인덱스 내의 일대일 필드로 쉽게 매핑할 수 있습니다. ‘locations’ 필드에는 위치 ID 집합과 위치 설명이 있는 위치 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-113">While the fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, the ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="6fd41-114">Azure Search에 이를 지원하는 데이터 형식이 없는 경우 다른 방법으로 Azure Search에서 모델링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-114">Given that Azure Search does not have a data type that supports this, we need a different way to model this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="6fd41-115">이 기술은 Kirk Evans의 블로그 게시물 [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/)(Azure Search를 사용하여 DocumentDB 인덱싱)에도 설명되어 있습니다. 여기에서 [컬렉션](https://msdn.microsoft.com/library/azure/dn798938.aspx)(또는 문자열 배열)인 `locationsID` 및 `locationsDescription`라는 필드가 있는 "데이터 평면화"라는 기술을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening the data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-the-array-into-individual-fields"></a><span data-ttu-id="6fd41-116">1부: 배열을 개별 필드로 평면화</span><span class="sxs-lookup"><span data-stu-id="6fd41-116">Part 1: Flatten the array into individual fields</span></span>
<span data-ttu-id="6fd41-117">이 데이터 집합을 제공하는 Azure Search 인덱스를 만들려면 중첩된 하위 구조에 대한 개별 필드 `locationsID` 및 `locationsDescription`을 [컬렉션](https://msdn.microsoft.com/library/azure/dn798938.aspx)(또는 문자열 배열)의 데이터 형식과 함께 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-117">To create an Azure Search index that accommodates this dataset, create individual fields for the nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="6fd41-118">이러한 필드에서 ‘1’ 및 ‘2’ 값을 John Smith의 `locationsID` 필드로, ‘3’ & ‘4’ 값을 Jen Campbell의 `locationsID` 필드로 인덱싱합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-118">In these fields you would index the values ‘1’ and ‘2’ into the `locationsID` field for John Smith and the values ‘3’ & ‘4’ into the `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="6fd41-119">Azure Search의 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-119">Your data within Azure Search would look like this:</span></span> 

![샘플 데이터, 2행](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-the-index-definition"></a><span data-ttu-id="6fd41-121">2단계: 인덱스 정의에 컬렉션 필드 추가</span><span class="sxs-lookup"><span data-stu-id="6fd41-121">Part 2: Add a collection field in the index definition</span></span>
<span data-ttu-id="6fd41-122">인덱스 스키마에서 필드 정의는 이 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-122">In the index schema, the field definitions might look similar to this example.</span></span>

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-the-index"></a><span data-ttu-id="6fd41-123">검색 동작의 유효성 검사 및 인덱스 확장(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="6fd41-123">Validate search behaviors and optionally extend the index</span></span>
<span data-ttu-id="6fd41-124">인덱스를 만들고 데이터를 로드한 후에는 해결 방법을 테스트하여 데이터 집합에 대한 검색 쿼리 실행을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-124">Assuming you created the index and loaded the data, you can now test the solution to verify search query execution against the dataset.</span></span> <span data-ttu-id="6fd41-125">각 **컬렉션** 필드는 **검색 가능**해야 하고, **필터링 가능**해야 하며 **패싯 가능**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="6fd41-126">다음과 같이 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-126">You should be able to run queries like:</span></span>

* <span data-ttu-id="6fd41-127">‘Adventureworks Headquarters’에서 근무하는 모든 사용자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-127">Find all people who work at the ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="6fd41-128">‘Home Office’에서 근무하는 사용자 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-128">Get a count of the number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="6fd41-129">‘Home Office’에서 근무하는 사용자 중 이들이 근무하는 다른 사무실과 각 위치의 사용자 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-129">Of the people who work at a ‘Home Office’, show what other offices they work along with a count of the people in each location.</span></span>  

<span data-ttu-id="6fd41-130">이 기술은 위치 ID와 위치 설명을 함께 사용하여 검색을 수행해야 할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-130">Where this technique falls apart is when you need to do a search that combines both the location id as well as the location description.</span></span> <span data-ttu-id="6fd41-131">예:</span><span class="sxs-lookup"><span data-stu-id="6fd41-131">For example:</span></span>

* <span data-ttu-id="6fd41-132">Home Office가 있고 위치 ID가 4인 사용자를 모두 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="6fd41-133">원본 콘텐츠를 회수하면 다음과 같은 모양이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-133">If you recall the original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="6fd41-134">그러나 이제 데이터가 개별 필드로 분류되어 Jen Campbell에 대한 Home Office가 `locationsID 3` 또는 `locationsID 4`에 연결된 것을 알 수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-134">However, now that we have separated the data into separate fields, we have no way of knowing if the Home Office for Jen Campbell relates to `locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="6fd41-135">이러한 경우 인덱스에서 모든 데이터를 단일 컬렉션으로 결합한 다른 필드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-135">To handle this case, define another field in the index that combines all of the data into a single collection.</span></span>  <span data-ttu-id="6fd41-136">이 예제에서는 이 필드를 `locationsCombined`라고 하고 `||`를 사용하여 콘텐츠를 분리합니다. 이때 콘텐츠에 고유한 문자 집합이라고 생각되는 다른 구분 기호를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-136">For our example, we will call this field `locationsCombined` and we will separate the content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="6fd41-137">예:</span><span class="sxs-lookup"><span data-stu-id="6fd41-137">For example:</span></span> 

![샘플 데이터, 구분 기호가 있는 2행](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="6fd41-139">이 `locationsCombined` 필드를 사용하여 다음과 같이 더 많은 쿼리를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="6fd41-140">‘Home Office’에서 근무하며 위치 ID가 ‘4’인 사용자 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="6fd41-141">‘Home Office’에서 근무하며 위치 ID가 ‘4’인 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="6fd41-142">제한 사항</span><span class="sxs-lookup"><span data-stu-id="6fd41-142">Limitations</span></span>
<span data-ttu-id="6fd41-143">이 기술은 여러 시나리오에서 유용하지만 모든 경우에 적용되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="6fd41-144">예:</span><span class="sxs-lookup"><span data-stu-id="6fd41-144">For example:</span></span>

1. <span data-ttu-id="6fd41-145">복합 데이터 형식에 정적 필드 집합이 없고 가능성 있는 모든 형식을 단일 필드에 매핑할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="6fd41-145">If you do not have a static set of fields in your complex data type and there was no way to map all the possible types to a single field.</span></span> 
2. <span data-ttu-id="6fd41-146">중첩된 개체를 업데이트하는 데 Azure Search 인덱스에서 업데이트해야 할 항목을 정확하게 결정하기 위해 추가 작업이 필요한 경우</span><span class="sxs-lookup"><span data-stu-id="6fd41-146">Updating the nested objects requires some extra work to determine exactly what needs to be updated in the Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="6fd41-147">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="6fd41-147">Sample code</span></span>
<span data-ttu-id="6fd41-148">복합 JSON 데이터 집합을 Azure Search로 인덱싱하고 이 [GitHub 리포지토리](https://github.com/liamca/AzureSearchComplexTypes)에서 이 데이터 집합에 대해 여러 가지 쿼리를 수행하는 방법에 대한 예를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-148">You can see an example on how to index a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="6fd41-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6fd41-149">Next step</span></span>
<span data-ttu-id="6fd41-150">[복합 데이터 형식의 기본 지원에 대해 응답](https://feedback.azure.com/forums/263029-azure-search) 하고 기능 구현과 관련하여 고려해야 할 추가 입력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on the Azure Search UserVoice page and provide any additional input that you’d like us to consider regarding feature implementation.</span></span> <span data-ttu-id="6fd41-151">Twitter를 통해 @liamca에 직접 연락할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd41-151">You can also reach out to me directly on Twitter at @liamca.</span></span>


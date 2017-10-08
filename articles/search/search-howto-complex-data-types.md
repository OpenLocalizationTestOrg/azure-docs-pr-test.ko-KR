---
title: "Azure 검색의 aaaHow toomodel 복잡 한 데이터 형식 | Microsoft Docs"
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
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a><span data-ttu-id="28271-103">Azure 검색의 toomodel 복잡 한 데이터 형식을 하는 방법</span><span class="sxs-lookup"><span data-stu-id="28271-103">How toomodel complex data types in Azure Search</span></span>
<span data-ttu-id="28271-104">외부 데이터 집합 사용 toopopulate Azure 검색 인덱스 연결 된 해제 되지 않도록 깔끔하게 테이블 형식의 행 집합을 계층적 또는 중첩 된 하위 구조체 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28271-104">External datasets used toopopulate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="28271-105">이러한 구조의 예에는 한 고객에 대한 여러 위치와 전화 번호, 단일 SKU에 대한 여러 색과 크기, 한 권의 책에 대한 여러 저자 등이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28271-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="28271-106">모델링 용어에 표시 될 수 있습니다 이러한 구조 참조 tooas *복잡 한 데이터 형식을*, *복합 데이터 형식*, *복합 데이터 형식*, 또는 *집계 데이터 형식*, 몇 가지 tooname 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-106">In modeling terms, you might see these structures referred tooas *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, tooname a few.</span></span>

<span data-ttu-id="28271-107">Azure 검색에서는 복잡 한 데이터 형식은 기본적으로 지원 되지 않습니다 되지만 hello 구조를 평면화 하 고 사용 하 여 다음의 2 단계 프로세스를 포함 하는 검증 된 문제를 해결 한 **컬렉션** 데이터 형식 tooreconstitute hello 내부 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="28271-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening hello structure and then using a **Collection** data type tooreconstitute hello interior structure.</span></span> <span data-ttu-id="28271-108">이 문서에서 설명 하는 hello 기법 다음 허용 hello 콘텐츠 toobe 검색 결과, 패싯, 필터링 및 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-108">Following hello technique described in this article allows hello content toobe searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="28271-109">복합 데이터 구조의 예</span><span class="sxs-lookup"><span data-stu-id="28271-109">Example of a complex data structure</span></span>
<span data-ttu-id="28271-110">일반적으로, 문제의 hello 데이터에는 Azure Cosmos DB와 같은 NoSQL 저장소에 있는 항목 또는 JSON 또는 XML 문서 집합으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28271-110">Typically, hello data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="28271-111">구조적으로 hello 챌린지 toobe 검색 하 고 필터링 해야 하는 여러 개의 자식 항목이 하는 것과 형태소 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-111">Structurally, hello challenge stems from having multiple child items that need toobe searched and filtered.</span></span>  <span data-ttu-id="28271-112">Hello 해결 방법을 설명 하는 시작 점으로 hello 예를 들어 연락처의 집합을 나열 하는 JSON 문서에 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-112">As a starting point for illustrating hello workaround, take hello following JSON document that lists a set of contacts as an example:</span></span>

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

<span data-ttu-id="28271-113">Hello 필드 라는 'id', 'name' 및 '회사' 쉽게 매핑할 수 있는 Azure 검색 인덱스 내에서 필드로 일대일, hello '위치' 필드 위치,으로 위치 Id 위치 설명 세트의 배열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-113">While hello fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, hello ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="28271-114">Azure 검색에서 지 원하는 데이터 형식에 없는 있다고 가정이 항목이 필요한 다른 방식으로 toomodel Azure 검색에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-114">Given that Azure Search does not have a data type that supports this, we need a different way toomodel this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="28271-115">이 기술은에 설명 되어 Kirk Evans 하 여 블로그 게시물을 [Azure 검색 DocumentDB 인덱싱](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), "flattening hello data" 라는 필드가 있는 그에 따라 기법을 보여 주는 `locationsID` 및 `locationsDescription` 모두 [컬렉션](https://msdn.microsoft.com/library/azure/dn798938.aspx) (또는 문자열의 배열)입니다.</span><span class="sxs-lookup"><span data-stu-id="28271-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening hello data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a><span data-ttu-id="28271-116">1 부: hello 배열 개별 필드로 결합</span><span class="sxs-lookup"><span data-stu-id="28271-116">Part 1: Flatten hello array into individual fields</span></span>
<span data-ttu-id="28271-117">이 데이터 집합을 제공 하는 Azure 검색 인덱스 toocreate hello 중첩된 구조에 대 한 개별 필드를 만들: `locationsID` 및 `locationsDescription` 의 데이터 형식과 [컬렉션](https://msdn.microsoft.com/library/azure/dn798938.aspx) (또는 문자열의 배열)입니다.</span><span class="sxs-lookup"><span data-stu-id="28271-117">toocreate an Azure Search index that accommodates this dataset, create individual fields for hello nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="28271-118">이러한 필드에 hello에 '1' 및 '2' hello 값 인덱스는 `locationsID` John Smith 및 hello 값 '3' & '4' hello에 대 한 필드 `locationsID` Jen Campbell에 대 한 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="28271-118">In these fields you would index hello values ‘1’ and ‘2’ into hello `locationsID` field for John Smith and hello values ‘3’ & ‘4’ into hello `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="28271-119">Azure Search의 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28271-119">Your data within Azure Search would look like this:</span></span> 

![샘플 데이터, 2행](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a><span data-ttu-id="28271-121">2 부: hello 인덱스 정의의 컬렉션 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-121">Part 2: Add a collection field in hello index definition</span></span>
<span data-ttu-id="28271-122">Hello 인덱스 스키마에 hello 필드 정의는 비슷한 예는 toothis 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28271-122">In hello index schema, hello field definitions might look similar toothis example.</span></span>

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

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a><span data-ttu-id="28271-123">검색 동작의 유효성을 검사 하 고 필요에 따라 hello 인덱스 확장</span><span class="sxs-lookup"><span data-stu-id="28271-123">Validate search behaviors and optionally extend hello index</span></span>
<span data-ttu-id="28271-124">만든된 hello 인덱스 및 hello 로드 된 데이터 라고 가정할 경우 hello 데이터 집합에 대 한 hello 솔루션 tooverify 검색 쿼리 실행을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28271-124">Assuming you created hello index and loaded hello data, you can now test hello solution tooverify search query execution against hello dataset.</span></span> <span data-ttu-id="28271-125">각 **컬렉션** 필드는 **검색 가능**해야 하고, **필터링 가능**해야 하며 **패싯 가능**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="28271-126">같은 쿼리 toorun 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-126">You should be able toorun queries like:</span></span>

* <span data-ttu-id="28271-127">' Adventureworks 본사 ' hello에서 근무 하는 모든 사용자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="28271-127">Find all people who work at hello ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="28271-128">' 홈 오피스 '에서 작업 하는 사람의 hello 개수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="28271-128">Get a count of hello number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="28271-129">' 홈 오피스 '에서 작업 하는 hello 인력, 각 위치에 hello 인원 수와 함께 작동 하는 다른 어떤 사무실을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28271-129">Of hello people who work at a ‘Home Office’, show what other offices they work along with a count of hello people in each location.</span></span>  

<span data-ttu-id="28271-130">이 기술은 떨어져 있는 대체 하는 것은 toodo 결합으로 hello 위치 id hello 위치 설명 하는 검색을 식별할 때.</span><span class="sxs-lookup"><span data-stu-id="28271-130">Where this technique falls apart is when you need toodo a search that combines both hello location id as well as hello location description.</span></span> <span data-ttu-id="28271-131">예:</span><span class="sxs-lookup"><span data-stu-id="28271-131">For example:</span></span>

* <span data-ttu-id="28271-132">Home Office가 있고 위치 ID가 4인 사용자를 모두 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="28271-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="28271-133">이 다음과 같이 hello 원본 콘텐츠를 기억 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="28271-133">If you recall hello original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="28271-134">그러나 이제 별도 필드로 hello 데이터 구분 했습니다, 있는지 hello Campbell Jen에 대 한 홈 오피스 너무 관련 된 것 이면 알 수 없습니다`locationsID 3` 또는 `locationsID 4`합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-134">However, now that we have separated hello data into separate fields, we have no way of knowing if hello Home Office for Jen Campbell relates too`locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="28271-135">이 경우 toohandle hello 데이터 모두를 하나의 컬렉션으로 결합 하는 hello 인덱스의 다른 필드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-135">toohandle this case, define another field in hello index that combines all of hello data into a single collection.</span></span>  <span data-ttu-id="28271-136">이 예에서는이 필드 라고 합니다 `locationsCombined` hello 콘텐츠를 구분할 म 및는 `||` 생각 하는 모든 구분 기호 문자 콘텐츠에 대 한 고유한 것을 선택할 수는 있지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-136">For our example, we will call this field `locationsCombined` and we will separate hello content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="28271-137">예:</span><span class="sxs-lookup"><span data-stu-id="28271-137">For example:</span></span> 

![샘플 데이터, 구분 기호가 있는 2행](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="28271-139">이 `locationsCombined` 필드를 사용하여 다음과 같이 더 많은 쿼리를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28271-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="28271-140">‘Home Office’에서 근무하며 위치 ID가 ‘4’인 사용자 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="28271-141">‘Home Office’에서 근무하며 위치 ID가 ‘4’인 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="28271-142">제한 사항</span><span class="sxs-lookup"><span data-stu-id="28271-142">Limitations</span></span>
<span data-ttu-id="28271-143">이 기술은 여러 시나리오에서 유용하지만 모든 경우에 적용되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28271-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="28271-144">예:</span><span class="sxs-lookup"><span data-stu-id="28271-144">For example:</span></span>

1. <span data-ttu-id="28271-145">복잡 한 데이터 형식에는 정적 필드 집합이 없는 되었으며 방법은 toomap 없는 경우 모든 hello 가능한 tooa 단일 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-145">If you do not have a static set of fields in your complex data type and there was no way toomap all hello possible types tooa single field.</span></span> 
2. <span data-ttu-id="28271-146">Hello Azure 검색 인덱스에서 업데이트 toobe 정확히 필요한 몇 가지 추가 작업 toodetermine 필요 중첩 hello 개체 업데이트</span><span class="sxs-lookup"><span data-stu-id="28271-146">Updating hello nested objects requires some extra work toodetermine exactly what needs toobe updated in hello Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="28271-147">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="28271-147">Sample code</span></span>
<span data-ttu-id="28271-148">예 설정 방법에 tooindex 복잡 한 JSON 데이터를 Azure 검색에 파악 하 고이이 데이터 집합을 통해 다양 한 쿼리를 수행할 [GitHub 리포지토리](https://github.com/liamca/AzureSearchComplexTypes)합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-148">You can see an example on how tooindex a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="28271-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28271-149">Next step</span></span>
<span data-ttu-id="28271-150">[복잡 한 데이터 형식에 대 한 기본 지원에 대 한 투표](https://feedback.azure.com/forums/263029-azure-search) hello Azure 검색 UserVoice 페이지 및 추가 입력을 제공할 싶다는 의사를 us tooconsider 기능 구현에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on hello Azure Search UserVoice page and provide any additional input that you’d like us tooconsider regarding feature implementation.</span></span> <span data-ttu-id="28271-151">에 Twitter에서 직접 toome 또한 교류할 수 @liamca합니다.</span><span class="sxs-lookup"><span data-stu-id="28271-151">You can also reach out toome directly on Twitter at @liamca.</span></span>


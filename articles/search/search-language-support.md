---
title: "Azure Search 여러 언어 | Microsoft Docs"
description: "Azure 검색은 Lucene 및 Microsoft 제공 자연어 처리 기술을 통해 56개 언어를 지원합니다."
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: dbbab31bac66ce73dbf9883992713a2c16581e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="73a30-103">Azure 검색에서 다국어 문서에 대한 인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="73a30-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="73a30-104">포털</span><span class="sxs-lookup"><span data-stu-id="73a30-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="73a30-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="73a30-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="73a30-106">.NET</span><span class="sxs-lookup"><span data-stu-id="73a30-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="73a30-107">인덱스 정의의 검색 가능한 필드에서 한 가지 속성만 설정하면 간단히 언어 분석기를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-107">Unleashing the power of language analyzers is as easy as setting one property on a searchable field in the index definition.</span></span> <span data-ttu-id="73a30-108">이제 포털에서 이 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-108">Now you can do this step in the portal.</span></span>

<span data-ttu-id="73a30-109">다음은 사용자가 인덱스 스키마를 정의할 수 있는 Azure 검색의 Azure 포털 블레이드의 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-109">Below are screenshots of the Azure Portal blades for Azure Search that allow users to define an index schema.</span></span> <span data-ttu-id="73a30-110">이 블레이드로부터 사용자가 모든 필드를 만들고 각각에 대한 분석기 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-110">From this blade, users can create all of the fields and set the analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73a30-111">처음부터 새 인덱스를 만들거나 새 필드를 기존 인덱스에 추가할 때처럼 필드 정의 중에 언어 분석기를 설정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-111">You can only set a language analyzer during field definition, as in when creating a new index from the ground up, or when adding a new field to an existing index.</span></span> <span data-ttu-id="73a30-112">필드를 만들 때 분석기를 포함한 모든 속성을 완전히 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-112">Make sure you fully specify all attributes, including the analyzer, while creating the field.</span></span> <span data-ttu-id="73a30-113">변경 내용을 저장한 후에는 속성을 편집하거나 분석기 형식을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-113">You won't be able to edit the attributes or change the analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="73a30-114">새 필드 정의</span><span class="sxs-lookup"><span data-stu-id="73a30-114">Define a new field definition</span></span>
1. <span data-ttu-id="73a30-115">[Azure Portal](https://portal.azure.com)에 로그인하고 검색 서비스의 서비스 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-115">Sign in to the [Azure portal](https://portal.azure.com) and open the service blade of your search service.</span></span>
2. <span data-ttu-id="73a30-116">서비스 대시보드 위쪽의 명령 모음에 있는 **인덱스 추가** 를 클릭하여 새 인덱스를 시작하거나, 기존 인덱스를 여러 기존 인덱스에 추가하는 새 필드에 대해 분석기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-116">Click **Add index** in the command bar at the top of the service dashboard to start a new index, or open an existing index to set an analyzer on new fields you're adding to an existing index.</span></span>
3. <span data-ttu-id="73a30-117">언어 분석기 선택을 위한 분석기 탭 등, 인덱스 스키마 정의 옵션을 제공하는 필드 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-117">The Fields blade appears, giving you options for defining the schema of the index, including the Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="73a30-118">필드에서 이름을 입력하고 데이터 형식을 선택하며 필드를 전체 텍스트 검색 가능, 검색 결과에서 검색 가능, 패싯 탐색 구조에서 사용 가능, 정렬 가능 등으로 표시하는 속성을 설정하여 필드 정의를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-118">In Fields, start a field definition by providing a name, choosing the data type, and setting attributes to mark the field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="73a30-119">다음 필드로 이동하기 전에 **분석기** 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-119">Before moving on to the next field, open the **Analyzer** tab.</span></span>

<span data-ttu-id="73a30-120">![][1]
*분석기를 선택하려면 필드 블레이드의 분석기 탭을 클릭합니다.*</span><span class="sxs-lookup"><span data-stu-id="73a30-120">![][1]
*To select an analyzer, click the Analyzer tab on the Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="73a30-121">분석기 선택</span><span class="sxs-lookup"><span data-stu-id="73a30-121">Choose an analyzer</span></span>
1. <span data-ttu-id="73a30-122">스크롤하여 정의하는 필드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-122">Scroll to find the field you are defining.</span></span>
2. <span data-ttu-id="73a30-123">필드를 **검색 가능**으로 표시하지 않은 경우 지금 확인란을 클릭하여 검색 가능으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-123">If you haven't marked the field as searchable, click the checkbox now to mark it as **Searchable**.</span></span>
3. <span data-ttu-id="73a30-124">분석기 영역을 클릭하여 사용 가능한 분석기 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-124">Click the Analyzer area to display the list of available analyzers.</span></span>
4. <span data-ttu-id="73a30-125">사용할 분석기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-125">Choose the analyzer you want to use.</span></span>

<span data-ttu-id="73a30-126">![][2]
*각 필드에 대해 지원되는 분석기 중 하나를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="73a30-126">![][2]
*Select one of the supported analyzers for each field*</span></span>

<span data-ttu-id="73a30-127">기본적으로 모든 검색 가능 필드에서는 언어 중립적인 [표준 Lucene 분석기](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-127">By default, all searchable fields use the [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="73a30-128">지원되는 전체 분석기 목록을 보려면 [Azure 검색의 언어 지원](https://msdn.microsoft.com/library/azure/dn879793.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73a30-128">To view the full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="73a30-129">필드에 대해 언어 분석기를 선택한 후에는 해당 필드의 모든 인덱싱 및 검색 요청에 해당 분석기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-129">Once the language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="73a30-130">다른 분석기를 사용하는 여러 필드에 대해 쿼리가 실행된 경우 이 쿼리는 각 필드에 부합하는 분석기를 통해 독립적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-130">When a query is issued against multiple fields using different analyzers, the query will be processed independently by the right analyzers for each field.</span></span>

<span data-ttu-id="73a30-131">전세계의 많은 웹 및 모바일 응용 프로그램 서버 사용자가 각기 다른 언어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-131">Many web and mobile applications serve users around the globe using different languages.</span></span> <span data-ttu-id="73a30-132">지원되는 각각의 언어에 대해 필드를 만들면 이러한 시나리오를 위한 인덱스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-132">It’s possible to define an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="73a30-133">![][3]
*지원되는 각 언어에 대한 설명 필드가 있는 인덱스 정의*</span><span class="sxs-lookup"><span data-stu-id="73a30-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="73a30-134">쿼리를 실행한 에이전트의 언어를 아는 경우 검색 요청의 범위를 **searchFields** 쿼리 매개 변수를 사용하여 특정 필드로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-134">If the language of the agent issuing a query is known, a search request can be scoped to a specific field using the **searchFields** query parameter.</span></span> <span data-ttu-id="73a30-135">다음 쿼리는 폴란드어로 된 설명에 대해서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-135">The following query will be issued only against the description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="73a30-136">**탐색기 검색** 을 사용하여 위에 표시된 것과 유사한 쿼리를 붙여 넣으면 포털에서 인덱스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-136">You can query your index from the portal, using **Search explorer** to paste in a query similar to the one shown above.</span></span> <span data-ttu-id="73a30-137">탐색기 검색은 서비스 블레이드의 명령 모음에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-137">Search explorer is available from the command bar in the service blade.</span></span> <span data-ttu-id="73a30-138">세부 정보는 [포털에서 Azure 검색 인덱스 쿼리](search-explorer.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="73a30-138">See [Query your Azure Search index in the portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="73a30-139">간혹 쿼리를 실행한 에이전트의 언어를 알지 못할 수 있습니다. 이 경우 모든 필드에 대해 동시에 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-139">Sometimes the language of the agent issuing a query is not known, in which case the query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="73a30-140">필요한 경우 [평가 프로필](https://msdn.microsoft.com/library/azure/dn798928.aspx)을 사용하여 특정 언어로 된 결과에 대한 우선 순위를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="73a30-141">아래 예에서는 영어 설명에서 찾은 일치 항목이 폴란드 및 프랑스어 항목 일치보다 상대적으로 높은 점수를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-141">In the example below, matches found in the description in English will be scored higher relative to matches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="73a30-142">.NET 개발자인 경우 [Azure 검색 .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search)를 사용하여 언어 분석기를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-142">If you're a .NET developer, note that you can configure language analyzers using the [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="73a30-143">최신 릴리스에는 Microsoft 언어 분석기에 대한 지원도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73a30-143">The latest release includes support for the Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png

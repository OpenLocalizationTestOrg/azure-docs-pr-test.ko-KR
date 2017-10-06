---
title: "검색 다중 언어 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="366dd-103">Azure 검색에서 다국어 문서에 대한 인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="366dd-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="366dd-104">포털</span><span class="sxs-lookup"><span data-stu-id="366dd-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="366dd-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="366dd-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="366dd-106">.NET</span><span class="sxs-lookup"><span data-stu-id="366dd-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="366dd-107">언어 분석기의 unleashing hello 전원 hello 인덱스 정의의 검색 가능한 필드에 대해 하나의 속성을 설정 하기만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-107">Unleashing hello power of language analyzers is as easy as setting one property on a searchable field in hello index definition.</span></span> <span data-ttu-id="366dd-108">이제 hello 포털에서이 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-108">Now you can do this step in hello portal.</span></span>

<span data-ttu-id="366dd-109">다음은 hello의 스크린 샷을 Azure 포털 블레이드 Azure 검색 인덱스 스키마 사용자 toodefine를 허용 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-109">Below are screenshots of hello Azure Portal blades for Azure Search that allow users toodefine an index schema.</span></span> <span data-ttu-id="366dd-110">이 블레이드 사용자가 모든 hello 필드를 만들 수을 각각의 hello 분석기 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-110">From this blade, users can create all of hello fields and set hello analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="366dd-111">설정할 수 있습니다만 언어 분석기 필드 정의 하는 동안에서 같이, 접지 hello에서 새 인덱스를 만들 때나 새 필드 tooan 기존 인덱스를 추가 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="366dd-111">You can only set a language analyzer during field definition, as in when creating a new index from hello ground up, or when adding a new field tooan existing index.</span></span> <span data-ttu-id="366dd-112">Hello 필드를 만드는 동안 hello 분석기 포함 된 모든 특성을 완전히 지정 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-112">Make sure you fully specify all attributes, including hello analyzer, while creating hello field.</span></span> <span data-ttu-id="366dd-113">Hello 특성 수 tooedit 일 또는 변경 내용을 저장 한 후에 hello 분석기 유형을 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-113">You won't be able tooedit hello attributes or change hello analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="366dd-114">새 필드 정의</span><span class="sxs-lookup"><span data-stu-id="366dd-114">Define a new field definition</span></span>
1. <span data-ttu-id="366dd-115">Toohello 로그인 [Azure 포털](https://portal.azure.com) 및 검색 서비스의 서비스 블레이드 열기 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-115">Sign in toohello [Azure portal](https://portal.azure.com) and open hello service blade of your search service.</span></span>
2. <span data-ttu-id="366dd-116">클릭 **인덱스 추가** hello 명령에서 새 인덱스를 hello 서비스 대시보드 toostart hello 최상위에 가로 막대형 또는 기존 인덱스 tooset 새 필드를 추가 하는 분석기를 열고 tooan 기존 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-116">Click **Add index** in hello command bar at hello top of hello service dashboard toostart a new index, or open an existing index tooset an analyzer on new fields you're adding tooan existing index.</span></span>
3. <span data-ttu-id="366dd-117">hello 필드 블레이드에 표시 되 면 선택 언어 분석기에 대 한 사용 hello 분석기 탭을 포함 하 여 hello 인덱스의 hello 스키마 정의 대 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-117">hello Fields blade appears, giving you options for defining hello schema of hello index, including hello Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="366dd-118">필드에 설정 하 여 이름을 제공 하, hello 데이터 유형을 선택 하면 특성 toomark hello 필드 전체 텍스트로 검색 가능한, 패싯 탐색 구조에 사용할 수 있는 검색 결과에서 검색 가능한 sortable와 같은 필드 정의 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-118">In Fields, start a field definition by providing a name, choosing hello data type, and setting attributes toomark hello field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="366dd-119">Toohello 다음 필드를 이동 하기 전에 hello를 열고 **분석기** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-119">Before moving on toohello next field, open hello **Analyzer** tab.</span></span>

<span data-ttu-id="366dd-120">![][1]
*를 사용 하는 분석기 tooselect hello 필드 블레이드에서 hello 분석기 탭을 클릭*</span><span class="sxs-lookup"><span data-stu-id="366dd-120">![][1]
*tooselect an analyzer, click hello Analyzer tab on hello Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="366dd-121">분석기 선택</span><span class="sxs-lookup"><span data-stu-id="366dd-121">Choose an analyzer</span></span>
1. <span data-ttu-id="366dd-122">스크롤 toofind hello 필드를 정의 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-122">Scroll toofind hello field you are defining.</span></span>
2. <span data-ttu-id="366dd-123">검색 가능한 필드 hello로 표시 하지 않은 경우 클릭 hello 확인란 지금 toomark로 **Searchable**합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-123">If you haven't marked hello field as searchable, click hello checkbox now toomark it as **Searchable**.</span></span>
3. <span data-ttu-id="366dd-124">사용 가능한 분석기의 hello 분석기 영역 toodisplay hello 목록을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-124">Click hello Analyzer area toodisplay hello list of available analyzers.</span></span>
4. <span data-ttu-id="366dd-125">Hello 분석기 선택 toouse 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-125">Choose hello analyzer you want toouse.</span></span>

<span data-ttu-id="366dd-126">![][2]
*각 필드에 대해 지원 되는 hello 분석기 중 하나를 선택*</span><span class="sxs-lookup"><span data-stu-id="366dd-126">![][2]
*Select one of hello supported analyzers for each field*</span></span>

<span data-ttu-id="366dd-127">기본적으로 모든 검색 가능한 필드 사용 hello [표준 Lucene 분석기](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) 은 언어 중립적입니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-127">By default, all searchable fields use hello [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="366dd-128">tooview hello 전체 목록은 지원 분석기 [Azure 검색의 언어 지원](https://msdn.microsoft.com/library/azure/dn879793.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-128">tooview hello full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="366dd-129">필드에 대 한 hello 언어 분석기를 선택한 후 해당 필드에 대 한 각 인덱싱 및 검색 요청과 함께 사용 될지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-129">Once hello language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="366dd-130">다른 분석기를 사용 하 여 여러 필드에 대해 쿼리를 실행 하는 hello 쿼리 처리 됩니다 하지 독립적으로 각 필드에 대 한 hello 오른쪽 분석기에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-130">When a query is issued against multiple fields using different analyzers, hello query will be processed independently by hello right analyzers for each field.</span></span>

<span data-ttu-id="366dd-131">많은 웹 및 모바일 응용 프로그램에 서로 다른 언어를 사용 하 여 hello 세계 사용자가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-131">Many web and mobile applications serve users around hello globe using different languages.</span></span> <span data-ttu-id="366dd-132">시나리오에 대 한 인덱스를 이렇게 지원 되는 각 언어에 대 한 필드를 만들어 가능한 toodefine 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-132">It’s possible toodefine an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="366dd-133">![][3]
*지원되는 각 언어에 대한 설명 필드가 있는 인덱스 정의*</span><span class="sxs-lookup"><span data-stu-id="366dd-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="366dd-134">검색 요청 hello를 사용 하 여 범위 지정 된 tooa 특정 필드 수는 쿼리를 실행 하는 hello 에이전트의 hello 언어를 알 경우 **searchFields** 쿼리 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-134">If hello language of hello agent issuing a query is known, a search request can be scoped tooa specific field using hello **searchFields** query parameter.</span></span> <span data-ttu-id="366dd-135">hello 다음 쿼리 실행 될 폴란드어에 hello 설명에 대해서만:</span><span class="sxs-lookup"><span data-stu-id="366dd-135">hello following query will be issued only against hello description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="366dd-136">Hello 포털에서 인덱스를 쿼리할 수 있습니다를 사용 하 여 **탐색기 검색** 쿼리 비슷한 toohello 위의 예제에서 toopaste 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-136">You can query your index from hello portal, using **Search explorer** toopaste in a query similar toohello one shown above.</span></span> <span data-ttu-id="366dd-137">검색 탐색기는 hello 서비스 블레이드에서 hello 명령 모음에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-137">Search explorer is available from hello command bar in hello service blade.</span></span> <span data-ttu-id="366dd-138">참조 [hello 포털에서 Azure 검색 인덱스를 쿼리하여](search-explorer.md) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-138">See [Query your Azure Search index in hello portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="366dd-139">경우에 따라 hello는 쿼리를 실행 하는 hello 에이전트의 언어를 알 수 없는 사례는 hello에서 실행할 수 있습니다 모든 필드에 대해 동시에 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-139">Sometimes hello language of hello agent issuing a query is not known, in which case hello query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="366dd-140">필요한 경우 [평가 프로필](https://msdn.microsoft.com/library/azure/dn798928.aspx)을 사용하여 특정 언어로 된 결과에 대한 우선 순위를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="366dd-141">Hello 아래의 예제에서는 영어로 hello 설명에서 발견 된 일치 레코드 폴란드어 및 프랑스어에 더 높은 상대 toomatches를 점수가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-141">In hello example below, matches found in hello description in English will be scored higher relative toomatches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="366dd-142">.NET 개발자 인 경우 hello를 사용 하 여 언어 분석기를 구성할 수 있는지 확인 [Azure 검색.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search)합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-142">If you're a .NET developer, note that you can configure language analyzers using hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="366dd-143">hello 최신 릴리스는 hello Microsoft 언어 분석기도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="366dd-143">hello latest release includes support for hello Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png

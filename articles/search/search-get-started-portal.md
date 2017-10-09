---
<span data-ttu-id="ddd2a-101">제목: aaa "자습서: hello 포털에서 첫 번째 Azure 검색 인덱스를 만들기 | Microsoft Docs "설명: hello Azure 포털에서에서 사용 하 여 미리 정의 된 샘플 데이터 toogenerate 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-101">title: aaa"Tutorial: Create your first Azure Search index in hello portal | Microsoft Docs" description: In hello Azure portal, use predefined sample data toogenerate an index.</span></span> <span data-ttu-id="ddd2a-102">전체 텍스트 검색, 필터, 패싯, 유사 항목 검색, 지리적 검색 등을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-102">Explore full text search, filters, facets, fuzzy search, geosearch, and more.</span></span>
<span data-ttu-id="ddd2a-103">서비스: documentationcenter 검색: ' 작성자: HeidiSteen 관리자: jhubbard 편집기: ' 태그: azure 포털</span><span class="sxs-lookup"><span data-stu-id="ddd2a-103">services: search documentationcenter: '' author: HeidiSteen manager: jhubbard editor: '' tags: azure-portal</span></span>

<span data-ttu-id="ddd2a-104">ms.assetid: 21adc351-69bb-4a39-bc59-598c60c8f958 ms.service: ms.devlang 검색: na ms.workload: 검색 ms.topic: 문서 hero ms.tgt_pltfrm: na ms.date: 06/26/2017 ms.author: heidist</span><span class="sxs-lookup"><span data-stu-id="ddd2a-104">ms.assetid: 21adc351-69bb-4a39-bc59-598c60c8f958 ms.service: search ms.devlang: na ms.workload: search ms.topic: hero-article ms.tgt_pltfrm: na ms.date: 06/26/2017 ms.author: heidist</span></span>

---
# <a name="tutorial-create-your-first-azure-search-index-in-hello-portal"></a><span data-ttu-id="ddd2a-105">자습서: hello 포털에서 첫 번째 Azure 검색 인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="ddd2a-105">Tutorial: Create your first Azure Search index in hello portal</span></span>

<span data-ttu-id="ddd2a-106">Hello Azure 포털에서에서 미리 정의 된 샘플 데이터 집합 tooquickly로 시작은 hello를 사용 하 여 인덱스 생성 **데이터를 가져올** 마법사.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-106">In hello Azure portal, start with a predefined sample dataset tooquickly generate an index using hello **Import data** wizard.</span></span> <span data-ttu-id="ddd2a-107">**검색 탐색기**를 사용하여 전체 텍스트 검색, 필터, 패싯, 유사 항목 검색, 지리적 검색을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-107">Explore full text search, filters, facets, fuzzy search, and geosearch with **Search explorer**.</span></span>  

<span data-ttu-id="ddd2a-108">이 코드 없는 소개문에서는 흥미로운 쿼리를 바로 작성할 수 있도록 미리 정의된 데이터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-108">This code-free introduction gets you started with predefined data so that you can write interesting queries right away.</span></span> <span data-ttu-id="ddd2a-109">포털 도구는 코드를 대체하는 것은 아니지만 다음 작업에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-109">While portal tools are not a substitute for code, tools are useful for these tasks:</span></span>

+ <span data-ttu-id="ddd2a-110">최소의 노력으로 실습 학습</span><span class="sxs-lookup"><span data-stu-id="ddd2a-110">Hands on learning with minimal ramp-up</span></span>
+ <span data-ttu-id="ddd2a-111">**데이터 가져오기**로 코드를 작성하기 전에 인덱스 프로토타입 제작</span><span class="sxs-lookup"><span data-stu-id="ddd2a-111">Prototype an index before you write code in **Import data**</span></span>
+ <span data-ttu-id="ddd2a-112">**검색 탐색기**에서 쿼리 및 구분 분석 구문 테스트</span><span class="sxs-lookup"><span data-stu-id="ddd2a-112">Test queries and parser syntax in **Search explorer**</span></span>
+ <span data-ttu-id="ddd2a-113">기존 보기 인덱스 tooyour 게시 된 서비스 및 해당 특성을 조회</span><span class="sxs-lookup"><span data-stu-id="ddd2a-113">View an existing index published tooyour service and look up its attributes</span></span>

<span data-ttu-id="ddd2a-114">**예상 시간:** 약 15분. 계정 또는 서비스 등록이 필요할 시 더 길어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-114">**Time Estimate:** About 15 minutes, but longer if account or service sign-up is also required.</span></span> 

<span data-ttu-id="ddd2a-115">또는 사용 하 여 성능을 향상 시키는 한 [.NET에서 Azure 검색 소개 코드 기반 tooprogramming](search-howto-dotnet-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-115">Alternatively, ramp up using a [code-based introduction tooprogramming Azure Search in .NET](search-howto-dotnet-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddd2a-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ddd2a-116">Prerequisites</span></span>

<span data-ttu-id="ddd2a-117">이 자습서에서는 [Azure 구독](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) 및 [Azure Search 서비스](search-create-service-portal.md)를 사용하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-117">This tutorial assumes an [Azure subscription](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and [Azure Search service](search-create-service-portal.md).</span></span> 

<span data-ttu-id="ddd2a-118">서비스 tooprovision을 즉시 않으려면 볼 수 있습니다이 자습서의 단계를 hello의 6 분 데모가 약 3 분에서 시작 [Azure 검색 개요 비디오](https://channel9.msdn.com/Events/Connect/2016/138)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-118">If you don't want tooprovision a service immediately, you can watch a 6-minute demonstration of hello steps in this tutorial, starting at about three minutes into this [Azure Search Overview video](https://channel9.msdn.com/Events/Connect/2016/138).</span></span>

## <a name="find-your-service"></a><span data-ttu-id="ddd2a-119">서비스 찾기</span><span class="sxs-lookup"><span data-stu-id="ddd2a-119">Find your service</span></span>
1. <span data-ttu-id="ddd2a-120">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ddd2a-121">Azure 검색 서비스의 hello 서비스 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-121">Open hello service dashboard of your Azure Search service.</span></span> <span data-ttu-id="ddd2a-122">Hello 서비스 타일 tooyour 대시보드를 고정 하지 않은 경우 이런 방식이으로 서비스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-122">If you didn't pin hello service tile tooyour dashboard, you can find your service this way:</span></span> 
   
   * <span data-ttu-id="ddd2a-123">Hello Jumpbar, 클릭 **더 많은 서비스** hello hello 왼쪽된 탐색 창 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-123">In hello Jumpbar, click **More services** at hello bottom of hello left navigation pane.</span></span>
   * <span data-ttu-id="ddd2a-124">Hello 검색 상자에 입력 *검색* tooget 구독에 대 한 서비스 검색의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-124">In hello search box, type *search* tooget a list of search services for your subscription.</span></span> <span data-ttu-id="ddd2a-125">서비스는 hello 목록에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-125">Your service should appear in hello list.</span></span> 

## <a name="check-for-space"></a><span data-ttu-id="ddd2a-126">공간 확인</span><span class="sxs-lookup"><span data-stu-id="ddd2a-126">Check for space</span></span>
<span data-ttu-id="ddd2a-127">많은 고객 hello 무료 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-127">Many customers start with hello free service.</span></span> <span data-ttu-id="ddd2a-128">이 버전이 제한 toothree 인덱스, 데이터 원본 3 및 3 개의 인덱서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-128">This version is limited toothree indexes, three data sources, and three indexers.</span></span> <span data-ttu-id="ddd2a-129">시작하기 전에 추가 항목에 대한 공간이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-129">Make sure you have room for extra items before you begin.</span></span> <span data-ttu-id="ddd2a-130">이 자습서에서는 각 개체를 하나씩 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-130">This tutorial creates one of each object.</span></span> 

> [!TIP] 
> <span data-ttu-id="ddd2a-131">Hello 서비스 대시보드의 타일이 이미 있는 인덱스, 인덱서 및 데이터 원본 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-131">Tiles on hello service dashboard show how many indexes, indexers, and data sources you already have.</span></span> <span data-ttu-id="ddd2a-132">hello 인덱서 타일 성공 및 실패 표시기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-132">hello Indexer tile shows success and failure indicators.</span></span> <span data-ttu-id="ddd2a-133">Hello 타일 tooview hello 인덱서 개수를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-133">Click hello tile tooview hello indexer count.</span></span> 
>
> ![인덱서 및 데이터 원본에 대한 타일][1]
>

## <span data-ttu-id="ddd2a-135"><a name="create-index"></a> 인덱스 및 부하 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="ddd2a-135"><a name="create-index"></a> Create an index and load data</span></span>
<span data-ttu-id="ddd2a-136">특정 검색 동작을 최적화하는 데 사용되는 검색 가능한 데이터, 메타데이터 및 구문을 포함하는 *인덱스* 에 검색 쿼리가 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-136">Search queries iterate over an *index* containing searchable data, metadata, and constructs used for optimizing certain search behaviors.</span></span>

<span data-ttu-id="ddd2a-137">tookeep hello 통해 인덱서를 사용 하 여 탐색할 수 있는 기본 제공 된 샘플 데이터 집합 사용 포털 기반이 태스크에서는 **데이터를 가져올** 마법사.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-137">tookeep this task portal-based, we use a built-in sample dataset that can be crawled using an indexer via hello **Import data** wizard.</span></span> 

#### <a name="step-1-start-hello-import-data-wizard"></a><span data-ttu-id="ddd2a-138">1 단계: hello 데이터 가져오기 마법사 시작</span><span class="sxs-lookup"><span data-stu-id="ddd2a-138">Step 1: Start hello Import data wizard</span></span>
1. <span data-ttu-id="ddd2a-139">Azure 검색 서비스 대시보드에 클릭 **데이터를 가져올** hello 명령 모음 toostart를 만들고 인덱스 정보를 표시 하는 마법사에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-139">On your Azure Search service dashboard, click **Import data** in hello command bar toostart a wizard that both creates and populates an index.</span></span>
   
    ![데이터 가져오기 명령][2]

2. <span data-ttu-id="ddd2a-141">Hello 마법사에서 **데이터 소스** > **샘플** > **realestate 미국-표본**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-141">In hello wizard, click **Data Source** > **Samples** > **realestate-us-sample**.</span></span> <span data-ttu-id="ddd2a-142">이 데이터 원본은 이름, 형식 및 연결 정보를 통해 미리 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-142">This data source is preconfigured with a name, type, and connection information.</span></span> <span data-ttu-id="ddd2a-143">생성되는 데이터 원본은 다른 가져오기 작업에서 다시 사용할 수 있는 "기존 데이터 원본"이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-143">Once created, it becomes an "existing data source" that can be reused in other import operations.</span></span>

    ![샘플 데이터 집합 선택][9]

3. <span data-ttu-id="ddd2a-145">클릭 **확인** toouse 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-145">Click **OK** toouse it.</span></span>

#### <a name="step-2-define-hello-index"></a><span data-ttu-id="ddd2a-146">2 단계: hello 인덱스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-146">Step 2: Define hello index</span></span>
<span data-ttu-id="ddd2a-147">인덱스를 만들면 일반적으로 수동 및 코드 기반 이지만 hello 마법사 크롤링할 수는 모든 데이터 원본에 대 한 인덱스를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-147">Creating an index is typically manual and code-based, but hello wizard can generate an index for any data source it can crawl.</span></span> <span data-ttu-id="ddd2a-148">최소한, 인덱스 필요 이름과 fields 컬렉션, 문서 키 toouniquely hello로 표시 된 필드가 하나 있는 각 문서를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-148">Minimally, an index requires a name, and a fields collection, with one field marked as hello document key toouniquely identify each document.</span></span>

<span data-ttu-id="ddd2a-149">필드에는 데이터 유형과 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-149">Fields have data types and attributes.</span></span> <span data-ttu-id="ddd2a-150">hello 위쪽 hello 확인란은 *특성 인덱스* hello 필드는 사용 하는 방법을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-150">hello check boxes across hello top are *index attributes* controlling how hello field is used.</span></span> 

* <span data-ttu-id="ddd2a-151">**조회 가능** 은 검색 결과 목록에 표시된다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-151">**Retrievable** means that it shows up in search results list.</span></span> <span data-ttu-id="ddd2a-152">예를 들어 필드가 필터 식에만 사용되는 경우 이 확인란을 지워 검색 결과에 대한 제한 해제로 개별 필드를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-152">You can mark individual fields as off limits for search results by clearing this checkbox, for example when fields used only in filter expressions.</span></span> 
* <span data-ttu-id="ddd2a-153">**필터링 가능**, **정렬 가능** 및 **패싯 가능**은 필드를 필터, 정렬 또는 패싯 탐색 구조에 사용할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-153">**Filterable**, **Sortable**, and **Facetable** determine whether a field can be used in a filter, a sort, or a facet navigation structure.</span></span> 
* <span data-ttu-id="ddd2a-154">**검색 가능** 은 필드가 전체 텍스트 검색에 포함된다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-154">**Searchable** means that a field is included in full text search.</span></span> <span data-ttu-id="ddd2a-155">문자열은 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-155">Strings are searchable.</span></span> <span data-ttu-id="ddd2a-156">숫자 필드와 부울 필드는 종종 검색할 수 없다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-156">Numeric fields and Boolean fields are often marked as not searchable.</span></span> 

<span data-ttu-id="ddd2a-157">기본적으로 hello 마법사 hello 키 필드에 대 한 hello 기반으로 고유 식별자에 대 한 hello 데이터 소스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-157">By default, hello wizard scans hello data source for unique identifiers as hello basis for hello key field.</span></span> <span data-ttu-id="ddd2a-158">문자열은 검색 가능한 것으로 규정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-158">Strings are attributed as retrievable and searchable.</span></span> <span data-ttu-id="ddd2a-159">정수는 검색 가능하고, 필터링 가능하고, 정렬 가능하고, 패싯 가능한 것으로 규정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-159">Integers are attributed as retrievable, filterable, sortable, and facetable.</span></span>

  ![생성된 realestate 인덱스][3]

<span data-ttu-id="ddd2a-161">클릭 **확인** toocreate hello 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-161">Click **OK** toocreate hello index.</span></span>

#### <a name="step-3-define-hello-indexer"></a><span data-ttu-id="ddd2a-162">3 단계: hello 인덱서를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-162">Step 3: Define hello indexer</span></span>
<span data-ttu-id="ddd2a-163">Hello에 여전히 **데이터를 가져올** 마법사를 클릭 하 여 **인덱서** > **이름**, hello 인덱서에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-163">Still in hello **Import data** wizard, click **Indexer** > **Name**, and type a name for hello indexer.</span></span> 

<span data-ttu-id="ddd2a-164">이 개체는 실행 가능한 프로세스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-164">This object defines an executable process.</span></span> <span data-ttu-id="ddd2a-165">수를 배치 하는 되풀이 일정에 따라 하지만 지금 사용 하 여 hello 기본 옵션 toorun hello 인덱서에 대 한 즉시 클릭 한 후 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-165">You could put it on recurring schedule, but for now use hello default option toorun hello indexer once, immediately, when you click **OK**.</span></span>  

  ![realestate 인덱서][8]

## <a name="check-progress"></a><span data-ttu-id="ddd2a-167">진행 확인</span><span class="sxs-lookup"><span data-stu-id="ddd2a-167">Check progress</span></span>
<span data-ttu-id="ddd2a-168">toomonitor 데이터 가져오기, toohello 서비스 대시보드 돌아가서, 아래로 스크롤하여 및 hello를 두 번 클릭 **인덱서** 타일 tooopen hello 인덱서 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-168">toomonitor data import, go back toohello service dashboard, scroll down, and double-click hello **Indexers** tile tooopen hello indexers list.</span></span> <span data-ttu-id="ddd2a-169">새로 만든 hello 인덱서 상태를 나타내는 함께 hello 목록에 표시 되어야 "진행 중" 또는 hello 인덱싱된 문서 수와 함께 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-169">You should see hello newly created indexer in hello list, with status indicating "in progress" or success, along with hello number of documents indexed.</span></span>

   ![인덱서 진행 메시지][4]

## <span data-ttu-id="ddd2a-171"><a name="query-index"></a>쿼리 hello 인덱스</span><span class="sxs-lookup"><span data-stu-id="ddd2a-171"><a name="query-index"></a> Query hello index</span></span>
<span data-ttu-id="ddd2a-172">준비 tooquery에 있는 검색 인덱스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-172">You now have a search index that's ready tooquery.</span></span> <span data-ttu-id="ddd2a-173">**탐색기 검색** hello 포털에 기본 제공 되는 쿼리 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-173">**Search explorer** is a query tool built into hello portal.</span></span> <span data-ttu-id="ddd2a-174">검색 결과가 예상과 일치하는지 확인할 수 있도록 검색 상자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-174">It provides a search box so that you can verify whether search results are what you expect.</span></span> 

> [!TIP]
> <span data-ttu-id="ddd2a-175">Hello에 [Azure 검색 개요 비디오](https://channel9.msdn.com/Events/Connect/2016/138), 단계를 수행 하는 hello hello 비디오로 6m08s에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-175">In hello [Azure Search Overview video](https://channel9.msdn.com/Events/Connect/2016/138), hello following steps are demonstrated at 6m08s into hello video.</span></span>
>

1. <span data-ttu-id="ddd2a-176">클릭 **탐색기 검색** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-176">Click **Search explorer** on hello command bar.</span></span>

   ![검색 탐색기 명령][5]

2. <span data-ttu-id="ddd2a-178">클릭 **변경 인덱스** hello에 명령 모음 tooswitch 너무*realestate 미국-표본*합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-178">Click **Change index** on hello command bar tooswitch too*realestate-us-sample*.</span></span>

   ![인덱스 및 API 명령][6]

3. <span data-ttu-id="ddd2a-180">클릭 **설정 API 버전** hello REST Api는 사용할 수 있는 명령 모음 toosee에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-180">Click **Set API version** on hello command bar toosee which REST APIs are available.</span></span> <span data-ttu-id="ddd2a-181">Api 제공이 되는 아직 일반적으로 출시 toonew 기능을 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-181">Preview APIs give you access toonew features not yet generally released.</span></span> <span data-ttu-id="ddd2a-182">아래 hello 쿼리에 대 한 지시 하지 않는 hello 일반 공급 버전 (2016-09-01)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-182">For hello queries below, use hello generally available version (2016-09-01) unless directed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="ddd2a-183">[Azure 검색 REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents) 및 hello [.NET 라이브러리](search-howto-dotnet-sdk.md#core-scenarios) 완전히 동일 하지만 **탐색기 검색** 만 장착된 toohandle REST 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-183">[Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents) and hello [.NET library](search-howto-dotnet-sdk.md#core-scenarios) are fully equivalent, but **Search explorer** is only equipped toohandle REST calls.</span></span> <span data-ttu-id="ddd2a-184">모두에 대 한 구문을 허용 [단순 쿼리 구문을](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 및 [Lucene 쿼리 파서 전체](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), 검색 매개 변수에서 사용할 수 있는 모든 hello 및 [검색 문서](https://docs.microsoft.com/rest/api/searchservice/search-documents) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-184">It accepts syntax for both [simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) and [full Lucene query parser](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), plus all hello search parameters available in [Search Document](https://docs.microsoft.com/rest/api/searchservice/search-documents) operations.</span></span>
    > 

4. <span data-ttu-id="ddd2a-185">Hello 검색 표시줄에 아래 hello 쿼리 문자열을 입력 하 고 클릭 **검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-185">In hello search bar, enter hello query strings below and click **Search**.</span></span>

  ![검색 쿼리 예제][7]

**`search=seattle`**

+ <span data-ttu-id="ddd2a-187">hello `search` 매개 변수는 사용 되는 tooinput 키워드 검색 전체 텍스트 검색에 대 한이 예에서 킹 카운티, 워싱턴주의 목록을 반환, 포함 된 *시애틀* hello 문서의 검색 가능한 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-187">hello `search` parameter is used tooinput a keyword search for full text search, in this case, returning listings in King County, Washington state, containing *Seattle* in any searchable field in hello document.</span></span> 

+ <span data-ttu-id="ddd2a-188">**탐색기 검색** 자세한 정보 및 하드 tooread 변수가 문서 구조가 조밀한 열인 경우 JSON에 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-188">**Search explorer** returns results in JSON, which is verbose and hard tooread if documents have a dense structure.</span></span> <span data-ttu-id="ddd2a-189">문서에 따라 핸들 결과 tooextract 중요 한 요소를 검색 하는 toowrite 코드를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-189">Depending on your documents, you might need toowrite code that handles search results tooextract important elements.</span></span> 

+ <span data-ttu-id="ddd2a-190">문서는 hello 인덱스에서 검색 가능한 것으로 표시 하는 모든 필드의 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-190">Documents are composed of all fields marked as retrievable in hello index.</span></span> <span data-ttu-id="ddd2a-191">hello 포털에서 tooview 인덱스 특성 클릭 *realestate 미국-표본* hello에 **인덱스** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-191">tooview index attributes in hello portal, click *realestate-us-sample* in hello **Indexes** tile.</span></span>

**`search=seattle&$count=true&$top=100`**

+ <span data-ttu-id="ddd2a-192">hello `&` 기호는 사용 되는 tooappend 검색은 매개 변수를 임의의 순서로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-192">hello `&` symbol is used tooappend search parameters, which can be specified in any order.</span></span> 

+  <span data-ttu-id="ddd2a-193">hello `$count=true` 매개 변수는 반환 된 모든 문서의 hello 합계에 대 한 개수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-193">hello `$count=true` parameter returns a count for hello sum of all documents returned.</span></span> <span data-ttu-id="ddd2a-194">`$count=true`에서 보고하는 변경 내용을 모니터링하여 필터 쿼리를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-194">You can verify filter queries by monitoring changes reported by `$count=true`.</span></span> 

+ <span data-ttu-id="ddd2a-195">hello `$top=100` 반환 hello 가장 높은 순위 부족 hello 총 100 개의 문서를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-195">hello `$top=100` returns hello highest ranked 100 documents out of hello total.</span></span> <span data-ttu-id="ddd2a-196">기본적으로 Azure 검색 hello 처음 50 개 최상의 일치를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-196">By default, Azure Search returns hello first 50 best matches.</span></span> <span data-ttu-id="ddd2a-197">늘리거나 통해 hello 크기를 줄일 수 `$top`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-197">You can increase or decrease hello amount via `$top`.</span></span>

**`search=*&facet=city&$top=2`**

+ <span data-ttu-id="ddd2a-198">`search=*`는 빈 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-198">`search=*` is an empty search.</span></span> <span data-ttu-id="ddd2a-199">빈 검색은 모든 것을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-199">Empty searches search over everything.</span></span> <span data-ttu-id="ddd2a-200">빈 쿼리를 필터링 너무 제출 또는 패싯 hello 전체 세트를 문서에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-200">One reason for submitting an empty query is too filter or facet over hello complete set of documents.</span></span> <span data-ttu-id="ddd2a-201">예를 들어 hello 인덱스의 모든 도시 패싯 탐색 구조 tooconsist을 원하는합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-201">For example, you want a faceting navigation structure tooconsist of all cities in hello index.</span></span>

+  <span data-ttu-id="ddd2a-202">`facet`탐색 반환 구조체 tooa UI 컨트롤을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-202">`facet` returns a navigation structure that you can pass tooa UI control.</span></span> <span data-ttu-id="ddd2a-203">범주와 개수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-203">It returns categories and a count.</span></span> <span data-ttu-id="ddd2a-204">이 경우 범주 hello 다양 한 도시에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-204">In this case, categories are based on hello number of cities.</span></span> <span data-ttu-id="ddd2a-205">Azure Search에는 집계가 없습니다. 하지만 각 범주의 문서 수를 제공하는 `facet`을 통해 근사치를 집계할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-205">There is no aggregation in Azure Search, but you can approximate aggregation via `facet`, which gives a count of documents in each category.</span></span>

+ <span data-ttu-id="ddd2a-206">`$top=2`두 문서를 사용할 수 있는 방법을 저항력 `top` tooboth 줄이거나 결과 늘리십시오.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-206">`$top=2` brings back two documents, illustrating that you can use `top` tooboth reduce or increase results.</span></span>

**`search=seattle&facet=beds`**

+ <span data-ttu-id="ddd2a-207">이 쿼리는 *시애틀*에 대한 텍스트 검색에서 침대에 대한 패싯입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-207">This query is facet for beds, on a text search for *Seattle*.</span></span> <span data-ttu-id="ddd2a-208">`"beds"`목록 그룹 (방 3, 4 방와 목록)으로 분류에 적합 한, 패싯 hello 필드는 검색 가능한 것, filterable, 표시 되 고 값을 facetable hello 인덱스 및 hello에 있기 때문에 포함 (숫자, 1-5)으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-208">`"beds"` can be specified as a facet because hello field is marked as retrievable, filterable, and facetable in hello index, and hello values it contains (numeric, 1 through 5), are suitable for categorizing listings into groups (listings with 3 bedrooms, 4 bedrooms).</span></span> 

+ <span data-ttu-id="ddd2a-209">필터링 가능한 필드만 패싯이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-209">Only filterable fields can be faceted.</span></span> <span data-ttu-id="ddd2a-210">검색 가능 필드에만 hello 결과에 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-210">Only retrievable fields can be returned in hello results.</span></span>

**`search=seattle&$filter=beds gt 3`**

+ <span data-ttu-id="ddd2a-211">hello `filter` 매개 변수는 사용자가 제공한 hello 조건과 일치 하는 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-211">hello `filter` parameter returns results matching hello criteria you provided.</span></span> <span data-ttu-id="ddd2a-212">이 예에서는 침실 수가 3보다 큽니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-212">In this case, bedrooms greater than 3.</span></span> 

+ <span data-ttu-id="ddd2a-213">필터 구문은 OData 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-213">Filter syntax is an OData construction.</span></span> <span data-ttu-id="ddd2a-214">자세한 내용은 [OData 필터 구문](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-214">For more information, see [Filter OData syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search).</span></span>

**`search=granite countertops&highlight=description`**

+ <span data-ttu-id="ddd2a-215">Tooformatting 참조 적중 항목 강조 표시 텍스트에서 특정 필드에서 발견 되 hello 키워드 일치 하는 일치 항목을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-215">Hit highlighting refers tooformatting on text matching hello keyword, given matches are found in a specific field.</span></span> <span data-ttu-id="ddd2a-216">검색 단어는 깊이 설명에 포함 된, 적중 횟수 강조 toomake를 추가할 수 있습니다 것 보다 쉽게 toospot 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-216">If your search term is deeply buried in a description, you can add hit highlighting toomake it easier toospot.</span></span> <span data-ttu-id="ddd2a-217">이 경우 hello 포맷 구 `"granite countertops"` 쉽게 toosee hello 설명 필드에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-217">In this case, hello formatted phrase `"granite countertops"` is easier toosee in hello description field.</span></span>

**`search=mice&highlight=description`**

+ <span data-ttu-id="ddd2a-218">전체 텍스트 검색은 의미 체계가 유사한 단어 형태를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-218">Full text search finds word forms with similar semantics.</span></span> <span data-ttu-id="ddd2a-219">이 경우 검색 결과에 "mouse" 마우스 침입 "mice"에 대 한 응답 tooa 키워드 검색에 포함 된 홈에 대 한 강조 표시 된 텍스트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-219">In this case, search results contain highlighted text for "mouse", for homes that have mouse infestation, in response tooa keyword search on "mice".</span></span> <span data-ttu-id="ddd2a-220">여러 가지 형태의 hello 같은 단어가 언어 분석으로 인해 결과에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-220">Different forms of hello same word can appear in results because of linguistic analysis.</span></span> 

+ <span data-ttu-id="ddd2a-221">Azure Search는 Lucene와 Microsoft의 56가지 분석기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-221">Azure Search supports 56 analyzers from both Lucene and Microsoft.</span></span> <span data-ttu-id="ddd2a-222">Azure 검색에서 사용 하는 hello 기본값은 hello 표준 Lucene 분석기입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-222">hello default used by Azure Search is hello standard Lucene analyzer.</span></span> 

**`search=samamish`**

+ <span data-ttu-id="ddd2a-223">'Samamish' hello Samammish 고 원으로 hello 시애틀 지역에에서 대 한 같은 맞춤법이 틀린된 단어에는 일반적인 검색에서 일치 하는 tooreturn 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-223">Misspelled words, like 'samamish' for hello Samammish plateau in hello Seattle area, fail tooreturn matches in typical search.</span></span> <span data-ttu-id="ddd2a-224">toohandle 맞춤법 오류 hello 다음 예에 설명 된 유사 항목 검색을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-224">toohandle misspellings, you can use fuzzy search, described in hello next example.</span></span>

**`search=samamish~&queryType=full`**

+ <span data-ttu-id="ddd2a-225">Hello를 지정 하는 경우 유사 항목 검색을 사용 하도록 `~` hello 전체 쿼리 언어 구문 분석기는를 해석 하 고 hello을 올바르게 구문 분석을 사용 하 여 기호 `~` 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-225">Fuzzy search is enabled when you specify hello `~` symbol and use hello full query parser, which interprets and correctly parses hello `~` syntax.</span></span> 

+ <span data-ttu-id="ddd2a-226">유사 항목 검색을 설정할 때 발생 하는 hello 전체 쿼리 파서에서 선택 하는 경우에 사용할 수 `queryType=full`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-226">Fuzzy search is available when you opt in for hello full query parser, which occurs when you set `queryType=full`.</span></span> <span data-ttu-id="ddd2a-227">Hello 전체 쿼리 파서에서 사용 하도록 설정 하는 쿼리 시나리오에 대 한 자세한 내용은 참조 [Azure 검색의 쿼리 구문을 Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-227">For more information about query scenarios enabled by hello full query parser, see [Lucene query syntax in Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search).</span></span>

+ <span data-ttu-id="ddd2a-228">때 `queryType` 가 지정 되지 않은 경우 기본 단순 쿼리 파서 hello 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-228">When `queryType` is unspecified, hello default simple query parser is used.</span></span> <span data-ttu-id="ddd2a-229">hello 단순 쿼리 파서 빠릅니다 하지만 퍼지 검색, 정규식, 근접 검색 또는 고급 쿼리 유형도, 필요한 경우에 hello 전체 구문은 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-229">hello simple query parser is faster, but if you require fuzzy search, regular expressions, proximity search, or other advanced query types, you will need hello full syntax.</span></span> 

**`search=*&$count=true&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5`**

+ <span data-ttu-id="ddd2a-230">지리 공간 검색은 hello를 통해 지원 [edm입니다. 데이터 형식 GeographyPoint](https://docs.microsoft.com/rest/api/searchservice/supported-data-types) 좌표를 포함 하는 필드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-230">Geospatial search is supported through hello [edm.GeographyPoint data type](https://docs.microsoft.com/rest/api/searchservice/supported-data-types) on a field containing coordinates.</span></span> <span data-ttu-id="ddd2a-231">Geosearch는 [OData 필터 구문](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)에 지정된 필터 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-231">Geosearch is a type of filter, specified in [Filter OData syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search).</span></span> 

+ <span data-ttu-id="ddd2a-232">여기서 결과 보다 작은 5 킬로미터 (위도 및 경도 좌표도 지정) 하 여 주어진된 지점에서 위치 데이터에 대 한 모든 결과 필터링 하는 hello 예제 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-232">hello example query filters all results for positional data, where results are less than 5 kilometers from a given point (specified as latitude and longitude coordinates).</span></span> <span data-ttu-id="ddd2a-233">추가 하 여 `$count`, hello 거리 또는 hello 좌표 변경 개수 결과 반환을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-233">By adding `$count`, you can see how many results are returned when you change either hello distance or hello coordinates.</span></span> 

+ <span data-ttu-id="ddd2a-234">지리 공간 검색은 검색 응용 프로그램에 '주변 찾기' 기능이 있거나 지도 탐색을 사용하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-234">Geospatial search is useful if your search application has a 'find near me' feature or uses map navigation.</span></span> <span data-ttu-id="ddd2a-235">하지만 전체 텍스트 검색은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-235">It is not full text search, however.</span></span> <span data-ttu-id="ddd2a-236">국가 또는 도시 이름을 기준으로 검색 하는 것에 대 한 요구 사항을 사용자가 있으면 추가 toocoordinates에서 국가 또는 도시 이름이 포함 된 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-236">If you have user requirements for searching on a city or country by name, add fields containing city or country names, in addition toocoordinates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddd2a-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ddd2a-237">Next steps</span></span>

+ <span data-ttu-id="ddd2a-238">방금 만든 hello 개체 중 하나를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-238">Modify any of hello objects you just created.</span></span> <span data-ttu-id="ddd2a-239">Hello 마법사를 한 번 실행 한 후 다시 이동 하 고 확인 하거나 수정할 수 있습니다 개별 구성 요소: 인덱스, 인덱서 또는 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-239">After you run hello wizard once, you can go back and view or modify individual components: index, indexer, or data source.</span></span> <span data-ttu-id="ddd2a-240">Hello 필드 데이터 형식을 변경 하는 hello와 같은 일부 편집 hello 인덱스에서 허용 되지 않습니다 이지만 대부분 속성 및 설정은 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-240">Some edits, such as hello changing hello field data type, are not allowed on hello index, but most properties and settings are modifiable.</span></span>

  <span data-ttu-id="ddd2a-241">tooview 개별 구성 요소를 클릭 하 여 hello **인덱스**, **인덱서**, 또는 **데이터 원본** 바둑판식으로 배열 대시보드 toodisplay에서 기존 개체의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-241">tooview individual components, click hello **Index**, **Indexer**, or **Data Sources** tiles on your dashboard toodisplay a list of existing objects.</span></span> <span data-ttu-id="ddd2a-242">다시 작성, 필요 하지 않은 인덱스 편집에 대 한 더 toolearn 참조 [업데이트 인덱스 (Azure 검색 REST API)](https://docs.microsoft.com/rest/api/searchservice/update-index)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-242">toolearn more about index edits that do not require a rebuild, see [Update Index (Azure Search REST API)](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

+ <span data-ttu-id="ddd2a-243">Hello 도구와 다른 데이터 소스를 사용 하 여 단계를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-243">Try hello tools and steps with other data sources.</span></span> <span data-ttu-id="ddd2a-244">샘플 데이터 집합을 hello `realestate-us-sample`, Azure 검색 크롤링할 수 있는 Azure SQL 데이터베이스에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-244">hello sample dataset, `realestate-us-sample`, is from an Azure SQL Database that Azure Search can crawl.</span></span> <span data-ttu-id="ddd2a-245">Azure Search는 Azure SQL Database 외에도 Azure Table Storage, Blob Storage, Azure VM의 SQL Server, Azure Cosmos DB의 플랫 데이터 구조에서 인덱스를 크롤링하고 유추할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-245">Besides Azure SQL Database, Azure Search can crawl and infer an index from flat data structures in Azure Table storage, Blob storage, SQL Server on an Azure VM, and Azure Cosmos DB.</span></span> <span data-ttu-id="ddd2a-246">이러한 데이터 원본의 모든 hello 마법사에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-246">All of these data sources are supported in hello wizard.</span></span> <span data-ttu-id="ddd2a-247">코드에서 *인덱서*를 사용하여 간편하게 인덱스를 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-247">In code, you can populate an index easily using an *indexer*.</span></span>

+ <span data-ttu-id="ddd2a-248">다른 모든 비 인덱서 데이터 원본의 위치 코드 새로운 푸시하고 JSON tooyour 인덱스의 행 집합 변경 밀어 넣기 모델을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-248">All other non-indexer data sources are supported via a push model, where your code pushes new and changed rowsets in JSON tooyour index.</span></span> <span data-ttu-id="ddd2a-249">자세한 내용은 [Azure Search에서 문서 추가, 업데이트 또는 삭제](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-249">For more information, see [Add, update, or delete documents in Azure Search](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents).</span></span>

<span data-ttu-id="ddd2a-250">이 문서에 언급된 다른 기능에 대해 자세히 알아보려면 다음 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="ddd2a-250">Learn more about other features mentioned in this article by visiting these links:</span></span>

* [<span data-ttu-id="ddd2a-251">인덱서 개요</span><span class="sxs-lookup"><span data-stu-id="ddd2a-251">Indexers overview</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="ddd2a-252">Create Index (hello 인덱스 특성에 대 한 자세한 내용은 포함)</span><span class="sxs-lookup"><span data-stu-id="ddd2a-252">Create Index (includes a detailed explanation of hello index attributes)</span></span>](https://docs.microsoft.com/rest/api/searchservice/create-index)
* [<span data-ttu-id="ddd2a-253">검색 탐색기</span><span class="sxs-lookup"><span data-stu-id="ddd2a-253">Search Explorer</span></span>](search-explorer.md)
* [<span data-ttu-id="ddd2a-254">문서 검색(쿼리 구문의 예제 포함)</span><span class="sxs-lookup"><span data-stu-id="ddd2a-254">Search Documents (includes examples of query syntax)</span></span>](https://docs.microsoft.com/rest/api/searchservice/search-documents)


<!--Image references-->
[1]: ./media/search-get-started-portal/tiles-indexers-datasources2.png
[2]: ./media/search-get-started-portal/import-data-cmd2.png
[3]: ./media/search-get-started-portal/realestateindex2.png
[4]: ./media/search-get-started-portal/indexers-inprogress2.png
[5]: ./media/search-get-started-portal/search-explorer-cmd2.png
[6]: ./media/search-get-started-portal/search-explorer-changeindex-se2.png
[7]: ./media/search-get-started-portal/search-explorer-query2.png
[8]: ./media/search-get-started-portal/realestate-indexer2.png
[9]: ./media/search-get-started-portal/import-datasource-sample2.png
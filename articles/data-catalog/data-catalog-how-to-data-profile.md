---
title: "aaaHow tooData 프로 파일 데이터 원본"
description: "방법-tooarticle tooinclude 테이블 및 열 수준 데이터의 데이터 원본을 Azure Data Catalog에 등록 하는 경우 프로필 어떻게 및 어떻게 toouse 데이터 프로필 toounderstand 데이터 소스를 강조 표시 합니다."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="57106-103">데이터 원본 데이터 프로파일링</span><span class="sxs-lookup"><span data-stu-id="57106-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="57106-104">소개</span><span class="sxs-lookup"><span data-stu-id="57106-104">Introduction</span></span>
<span data-ttu-id="57106-105">**Microsoft Azure 데이터 카탈로그**는 등록 시스템 및 기업 데이터 원본을 위한 검색 시스템 역할을 하는 완전히 관리되는 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="57106-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="57106-106">즉, **Azure Data Catalog** 수 있도록 지 원하는 사용자에 대 한 모든 검색, 이해 하 고, 데이터 원본을 사용 하 고 기존 데이터에서 더 값 조직 tooget 수 있도록 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57106-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data.</span></span> <span data-ttu-id="57106-107">데이터 원본으로 등록 될 때 **Azure Data Catalog**hello 스토리 끝나지 있습니다 하지만 해당 메타 데이터를 복사 하 여 hello 서비스에 의해 인덱싱된, 합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span>

<span data-ttu-id="57106-108">hello **데이터 프로 파일링** 의 기능 **Azure Data Catalog** 카탈로그에서 지원 되는 데이터 원본의 hello 데이터를 검사 하 고 통계와 해당 데이터에 대 한 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-108">hello **Data Profiling** feature of **Azure Data Catalog** examines hello data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="57106-109">되기 쉬운 tooinclude 데이터 자산에 대 한 프로필.</span><span class="sxs-lookup"><span data-stu-id="57106-109">It's easy tooinclude a profile of your data assets.</span></span> <span data-ttu-id="57106-110">데이터 자산을 등록 하면 선택 **포함 데이터 프로필** hello 데이터 원본 등록 도구에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-110">When you register a data asset, choose **Include Data Profile** in hello data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="57106-111">데이터 프로파일링의 정의</span><span class="sxs-lookup"><span data-stu-id="57106-111">What is Data Profiling</span></span>
<span data-ttu-id="57106-112">데이터 프로 파일링 hello hello 데이터 원본의 데이터에 등록 되를 검사 하 고 통계와 해당 데이터에 대 한 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-112">Data profiling examines hello data in hello data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="57106-113">데이터 원본 검색 하는 동안 이러한 통계 확인할 수 있습니다 hello 데이터 toosolve의 hello 적합성 비즈니스 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="57106-113">During data source discovery, these statistics can help you determine hello suitability of hello data toosolve their business problem.</span></span>

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

<span data-ttu-id="57106-114">hello 다음 데이터 원본 지원 데이터 프로 파일링 합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-114">hello following data sources support data profiling:</span></span>

* <span data-ttu-id="57106-115">SQL Server(Azure SQL DB 및 Azure SQL 데이터 웨어하우스 포함) 테이블 및 뷰</span><span class="sxs-lookup"><span data-stu-id="57106-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="57106-116">Oracle 테이블 및 뷰</span><span class="sxs-lookup"><span data-stu-id="57106-116">Oracle tables and views</span></span>
* <span data-ttu-id="57106-117">Teradata 테이블 및 뷰</span><span class="sxs-lookup"><span data-stu-id="57106-117">Teradata tables and views</span></span>
* <span data-ttu-id="57106-118">Hive 테이블</span><span class="sxs-lookup"><span data-stu-id="57106-118">Hive tables</span></span>

<span data-ttu-id="57106-119">데이터 자산을 등록할 때 데이터 프로필을 포함하면 사용자가 다음을 비롯한 데이터 원본에 대한 질문에 대답하도록 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57106-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="57106-120">수 있는 비즈니스 문제 사용된 toosolve 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="57106-120">Can it be used toosolve my business problem?</span></span>
* <span data-ttu-id="57106-121">Tooparticular 표준 또는 패턴 hello 데이터 준수는?</span><span class="sxs-lookup"><span data-stu-id="57106-121">Does hello data conform tooparticular standards or patterns?</span></span>
* <span data-ttu-id="57106-122">Hello 비정상 hello 데이터 원본 중 일부 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="57106-122">What are some of hello anomalies of hello data source?</span></span>
* <span data-ttu-id="57106-123">내 응용 프로그램에 이 데이터를 통합할 경우 발생할 수 있는 문제는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="57106-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="57106-124">응용 프로그램으로 데이터를 통합 하는 방법을 설명서 tooan 자산 toodescribe를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57106-124">You can also add documentation tooan asset toodescribe how data could be integrated into an application.</span></span> <span data-ttu-id="57106-125">참조 [어떻게 toodocument 데이터 원본](data-catalog-how-to-documentation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-125">See [How toodocument data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="57106-126">데이터 원본을 등록할 때 tooinclude 데이터 프로 파일링 할 방법</span><span class="sxs-lookup"><span data-stu-id="57106-126">How tooinclude a data profile when registering a data source</span></span>
<span data-ttu-id="57106-127">되기 쉬운 tooinclude 데이터 원본에 대 한 프로필.</span><span class="sxs-lookup"><span data-stu-id="57106-127">It's easy tooinclude a profile of your data source.</span></span> <span data-ttu-id="57106-128">Hello에 데이터 소스를 등록 하면 **등록 개체 toobe** hello 데이터 원본 등록의 패널 도구를 선택 **포함 데이터 프로필**합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-128">When you register a data source, in hello **Objects toobe registered** panel of hello data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="57106-129">tooregister 데이터 원본을 참조 하는 방법에 대해 더 알아봅니다을 toolearn [어떻게 tooregister 데이터 원본](data-catalog-how-to-register.md) 및 [Azure Data Catalog 시작](data-catalog-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-129">toolearn more about how tooregister data sources, see [How tooregister data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="57106-130">데이터 프로필을 포함하는 데이터 자산에 대한 필터링</span><span class="sxs-lookup"><span data-stu-id="57106-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="57106-131">데이터 프로필을 포함 하는 toodiscover 데이터 자산을 포함 시킬 수 있습니다 `has:tableDataProfiles` 또는 `has:columnsDataProfiles` 검색 단어 중 하나로 합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-131">toodiscover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="57106-132">선택 하면 **포함 데이터 프로필** 테이블 및 열 수준 프로필 정보를 모두에 hello 데이터 원본 등록 도구를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-132">Selecting **Include Data Profile** in hello data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="57106-133">그러나 hello 데이터 카탈로그 API를 통해 데이터 자산 toobe 프로필 포함 되는 정보 집합을 하나만 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-133">However, hello Data Catalog API allows data assets toobe registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="57106-134">데이터 프로필 정보 보기</span><span class="sxs-lookup"><span data-stu-id="57106-134">Viewing data profile information</span></span>
<span data-ttu-id="57106-135">프로필에 적절 한 데이터 소스를 찾은 후 hello 데이터 프로필 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57106-135">Once you find a suitable data source with a profile, you can view hello data profile details.</span></span> <span data-ttu-id="57106-136">tooview hello 데이터 프로필을 선택 하는 데이터 자산 선택 **데이터 프로필** hello Data Catalog 포털 창에서.</span><span class="sxs-lookup"><span data-stu-id="57106-136">tooview hello data profile, select a data asset and choose **Data Profile** in hello Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="57106-137">**Azure Data Catalog** 의 데이터 프로필은 다음을 포함하여 테이블 및 열 프로필 정보를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="57106-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="57106-138">개체 데이터 프로필</span><span class="sxs-lookup"><span data-stu-id="57106-138">Object data profile</span></span>
* <span data-ttu-id="57106-139">행 수</span><span class="sxs-lookup"><span data-stu-id="57106-139">Number of rows</span></span>
* <span data-ttu-id="57106-140">테이블 크기</span><span class="sxs-lookup"><span data-stu-id="57106-140">Table size</span></span>
* <span data-ttu-id="57106-141">Hello 개체가 마지막으로 업데이트</span><span class="sxs-lookup"><span data-stu-id="57106-141">When hello object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="57106-142">열 데이터 프로필</span><span class="sxs-lookup"><span data-stu-id="57106-142">Column data profile</span></span>
* <span data-ttu-id="57106-143">열 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="57106-143">Column data type</span></span>
* <span data-ttu-id="57106-144">고유한 값 수</span><span class="sxs-lookup"><span data-stu-id="57106-144">Number of distinct values</span></span>
* <span data-ttu-id="57106-145">NULL 값이 있는 행 수</span><span class="sxs-lookup"><span data-stu-id="57106-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="57106-146">열 값에 대한 최소, 최대, 평균 및 표준 편차</span><span class="sxs-lookup"><span data-stu-id="57106-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="57106-147">요약</span><span class="sxs-lookup"><span data-stu-id="57106-147">Summary</span></span>
<span data-ttu-id="57106-148">데이터 프로 파일링 통계를 제공 하 고 정보에 대 한 등록 데이터 자산 toohelp hello 데이터 toosolve 비즈니스 문제의 hello 한지를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-148">Data profiling provides statistics and information about registered data assets toohelp you determine hello suitability of hello data toosolve business problems.</span></span> <span data-ttu-id="57106-149">주석 달기 및 데이터 원본을 문서화하는 작업과 함께 데이터 프로필은 사용자가 데이터를 잘 이해할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="57106-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="57106-150">참고 항목</span><span class="sxs-lookup"><span data-stu-id="57106-150">See Also</span></span>
* [<span data-ttu-id="57106-151">어떻게 tooregister 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="57106-151">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="57106-152">Azure Azure Data Catalog 시작</span><span class="sxs-lookup"><span data-stu-id="57106-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

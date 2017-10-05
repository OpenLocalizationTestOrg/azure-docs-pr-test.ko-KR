---
title: "데이터 원본을 데이터 프로파일링하는 방법"
description: "Azure Data Catalog에서 데이터 원본을 등록할 경우 테이블 및 열 수준 데이터 프로필을 포함하는 방법 및 데이터 프로필을 사용하여 데이터 원본을 이해하는 방법을 강조한 방법 문서입니다."
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
ms.openlocfilehash: 8f4174f0ed74706b8275c8b1f0a62753f2834fa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="8d7f4-103">데이터 원본 데이터 프로파일링</span><span class="sxs-lookup"><span data-stu-id="8d7f4-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="8d7f4-104">소개</span><span class="sxs-lookup"><span data-stu-id="8d7f4-104">Introduction</span></span>
<span data-ttu-id="8d7f4-105">**Microsoft Azure 데이터 카탈로그** 는 등록 시스템 및 기업 데이터 원본을 위한 검색 시스템 역할을 하는 완전히 관리되는 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="8d7f4-106">다시 말해서 **Azure 데이터 카탈로그** 는 사람들이 데이터 원본을 검색하고 이해하고 사용하도록 도우면서 조직의 기존 데이터로부터 더 많은 가치를 얻어내도록 돕는 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span></span> <span data-ttu-id="8d7f4-107">**Azure Data Catalog**를 사용하여 데이터 원본을 등록하면 해당 메타데이터를 복사하고 서비스로 인덱싱하지만 여기서 끝이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span>

<span data-ttu-id="8d7f4-108">**Azure Data Catalog**의 **데이터 프로파일링** 기능은 카탈로그에서 지원되는 데이터 원본에서 데이터를 검사하고 해당 데이터에 대한 통계 및 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-108">The **Data Profiling** feature of **Azure Data Catalog** examines the data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="8d7f4-109">데이터 자산의 프로필을 포함하는 것은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-109">It's easy to include a profile of your data assets.</span></span> <span data-ttu-id="8d7f4-110">데이터 자산을 등록하면 데이터 원본 등록 도구에서 **데이터 프로필 포함** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-110">When you register a data asset, choose **Include Data Profile** in the data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="8d7f4-111">데이터 프로파일링의 정의</span><span class="sxs-lookup"><span data-stu-id="8d7f4-111">What is Data Profiling</span></span>
<span data-ttu-id="8d7f4-112">데이터 프로파일링은 등록되는 데이터 원본에서 데이터를 검사하고 해당 데이터에 대한 통계와 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-112">Data profiling examines the data in the data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="8d7f4-113">데이터 원본을 검색하는 동안 이러한 통계는 데이터의 적합성을 결정하여 비즈니스 문제를 해결하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-113">During data source discovery, these statistics can help you determine the suitability of the data to solve their business problem.</span></span>

<!-- In [How to discover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How to include a data profile when registering a data source](#howto). -->

<span data-ttu-id="8d7f4-114">다음 데이터 원본은 데이터 프로파일링을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-114">The following data sources support data profiling:</span></span>

* <span data-ttu-id="8d7f4-115">SQL Server(Azure SQL DB 및 Azure SQL 데이터 웨어하우스 포함) 테이블 및 뷰</span><span class="sxs-lookup"><span data-stu-id="8d7f4-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="8d7f4-116">Oracle 테이블 및 뷰</span><span class="sxs-lookup"><span data-stu-id="8d7f4-116">Oracle tables and views</span></span>
* <span data-ttu-id="8d7f4-117">Teradata 테이블 및 뷰</span><span class="sxs-lookup"><span data-stu-id="8d7f4-117">Teradata tables and views</span></span>
* <span data-ttu-id="8d7f4-118">Hive 테이블</span><span class="sxs-lookup"><span data-stu-id="8d7f4-118">Hive tables</span></span>

<span data-ttu-id="8d7f4-119">데이터 자산을 등록할 때 데이터 프로필을 포함하면 사용자가 다음을 비롯한 데이터 원본에 대한 질문에 대답하도록 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="8d7f4-120">비즈니스 문제를 해결하는 데 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8d7f4-120">Can it be used to solve my business problem?</span></span>
* <span data-ttu-id="8d7f4-121">데이터가 특정 표준 또는 패턴을 확인하나요?</span><span class="sxs-lookup"><span data-stu-id="8d7f4-121">Does the data conform to particular standards or patterns?</span></span>
* <span data-ttu-id="8d7f4-122">일부 데이터 원본에서 비정상은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="8d7f4-122">What are some of the anomalies of the data source?</span></span>
* <span data-ttu-id="8d7f4-123">내 응용 프로그램에 이 데이터를 통합할 경우 발생할 수 있는 문제는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="8d7f4-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="8d7f4-124">응용 프로그램으로 데이터를 통합하는 방법을 설명하기 위해 자산에 문서를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-124">You can also add documentation to an asset to describe how data could be integrated into an application.</span></span> <span data-ttu-id="8d7f4-125">[데이터 원본을 문서화하는 방법](data-catalog-how-to-documentation.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-125">See [How to document data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-to-include-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="8d7f4-126">데이터 원본을 등록할 때 데이터 프로필을 포함하는 방법</span><span class="sxs-lookup"><span data-stu-id="8d7f4-126">How to include a data profile when registering a data source</span></span>
<span data-ttu-id="8d7f4-127">데이터 원본의 프로필을 포함하는 것은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-127">It's easy to include a profile of your data source.</span></span> <span data-ttu-id="8d7f4-128">데이터 원본에 등록할 때 데이터 원본 등록 도구의 **등록할 개체** 패널에서 **데이터 프로필 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-128">When you register a data source, in the **Objects to be registered** panel of the data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="8d7f4-129">데이터 원본을 등록하는 방법에 대해 자세히 알아보려면 [데이터 원본을 등록하는 방법](data-catalog-how-to-register.md) 및 [Azure Data Catalog 시작](data-catalog-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-129">To learn more about how to register data sources, see [How to register data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="8d7f4-130">데이터 프로필을 포함하는 데이터 자산에 대한 필터링</span><span class="sxs-lookup"><span data-stu-id="8d7f4-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="8d7f4-131">데이터 프로필을 포함하는 데이터 자산을 검색하려면 `has:tableDataProfiles` 또는 `has:columnsDataProfiles`를 검색 단어 중 하나로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-131">To discover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="8d7f4-132">데이터 원본 등록 도구에서 **데이터 프로필 포함** 을 선택하면 테이블 및 열 수준 프로필 정보가 모두 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-132">Selecting **Include Data Profile** in the data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="8d7f4-133">하지만 데이터 카탈로그 API를 통해 데이터 자산을 오직 하나 만의 프로필 정보 집합을 포함하여 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-133">However, the Data Catalog API allows data assets to be registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="8d7f4-134">데이터 프로필 정보 보기</span><span class="sxs-lookup"><span data-stu-id="8d7f4-134">Viewing data profile information</span></span>
<span data-ttu-id="8d7f4-135">프로필에 적합한 데이터 원본을 찾으면 데이터 프로필 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-135">Once you find a suitable data source with a profile, you can view the data profile details.</span></span> <span data-ttu-id="8d7f4-136">데이터 프로필을 보려면 데이터 자산을 선택하고 데이터 카탈로그 포털 창에서 **데이터 프로필** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-136">To view the data profile, select a data asset and choose **Data Profile** in the Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="8d7f4-137">**Azure Data Catalog** 의 데이터 프로필은 다음을 포함하여 테이블 및 열 프로필 정보를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="8d7f4-138">개체 데이터 프로필</span><span class="sxs-lookup"><span data-stu-id="8d7f4-138">Object data profile</span></span>
* <span data-ttu-id="8d7f4-139">행 수</span><span class="sxs-lookup"><span data-stu-id="8d7f4-139">Number of rows</span></span>
* <span data-ttu-id="8d7f4-140">테이블 크기</span><span class="sxs-lookup"><span data-stu-id="8d7f4-140">Table size</span></span>
* <span data-ttu-id="8d7f4-141">개체가 마지막으로 업데이트된 시기</span><span class="sxs-lookup"><span data-stu-id="8d7f4-141">When the object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="8d7f4-142">열 데이터 프로필</span><span class="sxs-lookup"><span data-stu-id="8d7f4-142">Column data profile</span></span>
* <span data-ttu-id="8d7f4-143">열 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="8d7f4-143">Column data type</span></span>
* <span data-ttu-id="8d7f4-144">고유한 값 수</span><span class="sxs-lookup"><span data-stu-id="8d7f4-144">Number of distinct values</span></span>
* <span data-ttu-id="8d7f4-145">NULL 값이 있는 행 수</span><span class="sxs-lookup"><span data-stu-id="8d7f4-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="8d7f4-146">열 값에 대한 최소, 최대, 평균 및 표준 편차</span><span class="sxs-lookup"><span data-stu-id="8d7f4-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="8d7f4-147">요약</span><span class="sxs-lookup"><span data-stu-id="8d7f4-147">Summary</span></span>
<span data-ttu-id="8d7f4-148">데이터 프로파일링은 등록된 데이터 자산에 대한 통계와 정보를 제공하여 비즈니스 문제를 해결하기 위해 데이터의 적합성을 결정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-148">Data profiling provides statistics and information about registered data assets to help you determine the suitability of the data to solve business problems.</span></span> <span data-ttu-id="8d7f4-149">주석 달기 및 데이터 원본을 문서화하는 작업과 함께 데이터 프로필은 사용자가 데이터를 잘 이해할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f4-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="8d7f4-150">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8d7f4-150">See Also</span></span>
* [<span data-ttu-id="8d7f4-151">데이터 원본을 등록하는 방법</span><span class="sxs-lookup"><span data-stu-id="8d7f4-151">How to register data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="8d7f4-152">Azure 데이터 카탈로그 시작</span><span class="sxs-lookup"><span data-stu-id="8d7f4-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

---
title: "'빅 데이터' 데이터 원본과 aaaHow toowork | Microsoft Docs"
description: "Azure Data Catalog를 사용 하 여 Azure Blob 저장소, Azure 데이터 레이크 Hadoop HDFS 등 '빅 데이터' 데이터 원본에 대 한 패턴을 강조 표시 하는 방법 tooarticle 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="db581-103">빅 데이터 관련 toowork 원본 Azure Data Catalog에 어떻게</span><span class="sxs-lookup"><span data-stu-id="db581-103">How toowork with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="db581-104">소개</span><span class="sxs-lookup"><span data-stu-id="db581-104">Introduction</span></span>
<span data-ttu-id="db581-105">**Microsoft Azure 데이터 카탈로그**는 등록 시스템 및 기업 데이터 원본을 위한 검색 시스템 역할을 하는 완전히 관리되는 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="db581-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="db581-106">핵심은 검색 이해 하 고 데이터 원본을 사용할 수 있도록 하 고 빅 데이터를 포함 하 여 자신의 기존 데이터 원본에서 조직의 tooget 더 많은 가치를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="db581-106">It is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="db581-107">**Azure Data Catalog** 지원 hello Azure 블로그 저장소의 blob 및 디렉터리와 Hadoop HDFS 파일 및 디렉터리를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db581-107">**Azure Data Catalog** supports hello registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="db581-108">hello 반 구조화 된 특성의 이러한 데이터 원본 뛰어난 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db581-108">hello semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="db581-109">그러나 tooget hello를 사용 하 여 등록에서 가장 많은 가치 **Azure Data Catalog**, 사용자가 hello 데이터 소스 구성 방법을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db581-109">However, tooget hello most value from registering them with **Azure Data Catalog**, users must consider how hello data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="db581-110">논리적 데이터 집합으로 디렉터리 처리</span><span class="sxs-lookup"><span data-stu-id="db581-110">Directories as logical data sets</span></span>
<span data-ttu-id="db581-111">빅 데이터 원본 구성을 위한 일반적인 방법은 논리 데이터 집합으로 tootreat 디렉터리 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db581-111">A common pattern for organizing big data sources is tootreat directories as logical data sets.</span></span> <span data-ttu-id="db581-112">최상위 디렉터리 하위 폴더에 파티션 정의 및 포함 된 hello 파일 자체 hello 데이터를 저장 하는 동안 사용 되는 toodefine 데이터 집합에는.</span><span class="sxs-lookup"><span data-stu-id="db581-112">Top-level directories are used toodefine a data set, while subfolders define partitions, and hello files they contain store hello data itself.</span></span>

<span data-ttu-id="db581-113">이 패턴의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db581-113">An example of this pattern might be:</span></span>

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

<span data-ttu-id="db581-114">이 예에서는 vehicle_maintenance_events 및 location_tracking_events가 논리 데이터 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="db581-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="db581-115">이러한 폴더 각각에는 년 및 월 단위로 하위 폴더에 정리된 데이터 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db581-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="db581-116">이러한 폴더 각각에는 수백 또는 수천 개의 파일이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db581-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="db581-117">이 패턴에서 개별 파일을 **Azure 데이터 카탈로그**에 등록해도 이를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db581-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="db581-118">의미 있는 toohello users hello 데이터로 작업 하는 hello 데이터 집합을 나타내는 hello 디렉터리를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db581-118">Instead, register hello directories that represent hello data sets that be meaningful toohello users working with hello data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="db581-119">참조 데이터 파일</span><span class="sxs-lookup"><span data-stu-id="db581-119">Reference data files</span></span>
<span data-ttu-id="db581-120">상호 보완적인 패턴에는 개별 파일로 toostore 참조 데이터 집합은입니다.</span><span class="sxs-lookup"><span data-stu-id="db581-120">A complementary pattern is toostore reference data sets as individual files.</span></span> <span data-ttu-id="db581-121">이러한 데이터 집합 빅 데이터의 hello '작은' 쪽으로 생각할 수 및 분석 데이터 모델에서 비슷한 toodimensions 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="db581-121">These data sets may be thought of as hello 'small' side of big data, and are often similar toodimensions in an analytical data model.</span></span> <span data-ttu-id="db581-122">참조 데이터 파일에는 레코드 hello 빅 데이터 저장소의 다른 위치에 저장 하는 hello 데이터 파일의 hello 대부분을 사용 하는 tooprovide 컨텍스트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="db581-122">Reference data files contain records that are used tooprovide context for hello bulk of hello data files stored elsewhere in hello big data store.</span></span>

<span data-ttu-id="db581-123">이 패턴의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db581-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="db581-124">참조 파일에 데이터는 hello 사용된 tooprovide 된 엔터티를 더 큰 데이터 hello에에서 이름 또는 ID로 tooonly 참조에 대 한 자세한 정보 수 분석가 나 데이터 과학자는 hello 큰 디렉터리 구조에 포함 된 hello 데이터를 사용할 때 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="db581-124">When an analyst or data scientist is working with hello data contained in hello larger directory structures, hello data in these reference files can be used tooprovide more detailed information for entities that are referred tooonly by name or ID in hello larger data set.</span></span>

<span data-ttu-id="db581-125">이 패턴에서는 의미가 있는 tooregister hello 개별 참조 데이터 파일 **Azure Data Catalog**합니다.</span><span class="sxs-lookup"><span data-stu-id="db581-125">In this pattern, it makes sense tooregister hello individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="db581-126">각 파일은 데이터 집합을 나타내며, 각각에 대해 개별적으로 주석을 추가하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db581-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="db581-127">대체 패턴</span><span class="sxs-lookup"><span data-stu-id="db581-127">Alternate patterns</span></span>
<span data-ttu-id="db581-128">hello hello 앞 섹션에서에서 설명 하는 패턴 방금 두 가지 가능한 큰 데이터 저장소를 구성할 수 있습니다 있지만 각 구현은 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="db581-128">hello patterns described in hello preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="db581-129">데이터 소스 구성 방법, 빅 데이터 원본으로 등록 하는 경우에 관계 없이 **Azure Data Catalog**, hello 파일 및 디렉터리 내에서 값 tooothers의 않는 hello 데이터 집합을 나타내는 등록에 집중 프로그램 조직입니다.</span><span class="sxs-lookup"><span data-stu-id="db581-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering hello files and directories that represent hello data sets that are of value tooothers within your organization.</span></span> <span data-ttu-id="db581-130">모든 파일 및 디렉터리 등록 hello 카탈로그, 관리가 어려울 toofind 사용자에 대 한가 필요한 복잡 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db581-130">Registering all files and directories can clutter hello catalog, making it harder for users toofind what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="db581-131">요약</span><span class="sxs-lookup"><span data-stu-id="db581-131">Summary</span></span>
<span data-ttu-id="db581-132">포함 된 데이터 원본 등록 **Azure Data Catalog** 쉽게 toodiscover 되도록 하 고 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="db581-132">Registering data sources with **Azure Data Catalog** makes them easier toodiscover and understand.</span></span> <span data-ttu-id="db581-133">등록 하 고 hello 빅 데이터 파일 및 디렉터리를 나타내는 논리 데이터 집합에 주석 지정를 찾아서 필요한 hello 빅 데이터 원본을 사용 하는 사용자가 도울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db581-133">By registering and annotating hello big data files and directories that represent logical data sets, you can help users find and use hello big data sources they need.</span></span>

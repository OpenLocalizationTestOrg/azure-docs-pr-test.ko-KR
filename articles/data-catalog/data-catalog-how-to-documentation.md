---
title: "aaaHow toodocument 데이터 소스 | Microsoft Docs"
description: "방법 tooarticle 강조 표시 방법을 toodocument 데이터 자산 Azure Data Catalog에 있습니다."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 4e46838d91ab4d0c0bc569ac526a0c729134bb10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="05f44-103">데이터 원본 문서화</span><span class="sxs-lookup"><span data-stu-id="05f44-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="05f44-104">소개</span><span class="sxs-lookup"><span data-stu-id="05f44-104">Introduction</span></span>
<span data-ttu-id="05f44-105">**Microsoft Azure 데이터 카탈로그**는 등록 시스템 및 기업 데이터 원본을 위한 검색 시스템 역할을 하는 완전히 관리되는 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="05f44-106">즉, **Azure Data Catalog** 을 검색할 수 있도록 모두는 *이해*, 데이터 원본을 사용 하 고 기존 데이터에서 값 추가 조직 tooget 수 있도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations tooget more value from their existing data.</span></span>

<span data-ttu-id="05f44-107">데이터 원본으로 등록 될 때 **Azure Data Catalog**hello 스토리 끝나지 있습니다 하지만 해당 메타 데이터를 복사 하 여 hello 서비스에 의해 인덱싱된, 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span> <span data-ttu-id="05f44-108">**Azure Data Catalog** hello 사용량과 hello 데이터 원본에 대 한 일반적인 시나리오를 설명 하는 전체 설명서가 자신의 사용자 tooprovide를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-108">**Azure Data Catalog** also allows users tooprovide their own complete documentation that can describe hello usage and common scenarios for hello data source.</span></span>

<span data-ttu-id="05f44-109">[어떻게 tooannotate 데이터 원본](data-catalog-how-to-annotate.md)는 hello 데이터 소스를 알고 있는 전문가 주석을 달 수 것 태그 및 설명을 사용 하 여는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-109">In [How tooannotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know hello data source can annotate it with tags and a description.</span></span> <span data-ttu-id="05f44-110">hello **Azure Data Catalog** 포털 사용자는 데이터 자산 및 컨테이너에 완벽 하 게 문서화할 수 있도록 서식 있는 텍스트 편집기에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-110">hello **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="05f44-111">hello 편집기 같은 단락 서식을 머리글의 텍스트 서식을 글머리 기호 목록, 번호 매기기 목록 및 테이블을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-111">hello editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="05f44-112">태그와 설명은 간단한 주석에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="05f44-113">그러나 toohelp 데이터 소비자는 데이터 원본의 hello 사용을 더 잘 이해 하 고 전문가 데이터 원본에 대 한 비즈니스 시나리오에서 완전 하 고 자세한 설명서를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-113">However, toohelp data consumers better understand hello use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="05f44-114">되기 쉬운 toodocument 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-114">It's easy toodocument a data source.</span></span> <span data-ttu-id="05f44-115">데이터 자산 또는 컨테이너를 선택하고 **설명서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="05f44-116">데이터 자산 문서화</span><span class="sxs-lookup"><span data-stu-id="05f44-116">Documenting data assets</span></span>
<span data-ttu-id="05f44-117">이점은 hello **Azure Data Catalog** 설명서 있습니다 toouse 데이터 자산의 전체 narrative 콘텐츠 리포지토리 toocreate로 데이터 카탈로그입니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-117">hello benefit of **Azure Data Catalog** documentation allows you toouse your Data Catalog as a content repository toocreate a complete narrative of your data assets.</span></span> <span data-ttu-id="05f44-118">컨테이너 및 테이블을 설명하는 자세한 내용을 둘러볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="05f44-119">SharePoint 또는 파일 공유와 같은 다른 콘텐츠 저장소의 콘텐츠를 이미 있는 경우이 기존 콘텐츠 toohello 자산 설명서 링크 tooreference를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-119">If you already have content in another content repository, such as SharePoint or a file share, you can add toohello asset documentation links tooreference this existing content.</span></span> <span data-ttu-id="05f44-120">이 기능을 사용해 기존 문서를 더 쉽게 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="05f44-121">설명서는 검색 인덱스에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="05f44-122">hello 설명서의 수준에서 까지입니다 hello 특성 및 값의 데이터를 설명 하는 자산 컨테이너 tooa 세부 설명 컨테이너 내에서 테이블 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-122">hello level of documentation can range from describing hello characteristics and value of a data asset container tooa detailed description of table schema within a container.</span></span> <span data-ttu-id="05f44-123">제공 된 설명서 hello 수준의 비즈니스 요구 사항에 따라 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-123">hello level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="05f44-124">하지만 데이터 자산을 문서화하는 일반적인 몇 가지 장단점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="05f44-125">단지 문서화: 모든 hello 콘텐츠를 한 곳에는 하지만 수 부족 필요한 세부 정보를 사용자 toomake 합리적인된 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-125">Document just a container: All hello content is in one place, but might lack necessary details for users toomake an informed decision.</span></span>
* <span data-ttu-id="05f44-126">방금 hello 테이블 문서: 콘텐츠 특정 toothat 개체가 아니라 사용자 문서에 대 한 여러 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-126">Document just hello tables: Content is specific toothat object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="05f44-127">컨테이너와 테이블을 문서화: 가장 포괄적인 접근 방식 있지만 hello 문서 관리가 더 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of hello documents.</span></span>

## <a name="summary"></a><span data-ttu-id="05f44-128">요약</span><span class="sxs-lookup"><span data-stu-id="05f44-128">Summary</span></span>
<span data-ttu-id="05f44-129">**Azure Data Catalog** 로 데이터 원본을 문서화하는 작업은 필요한 만큼의 세부 정보로 데이터 자산에 대한 설명을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="05f44-130">링크를 사용 하 여 통합 하는 기존 문서 및 데이터 자산에서 기존 콘텐츠 저장소에 저장 된 toocontent을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-130">By using links, you can link toocontent stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="05f44-131">사용자가 적절한 데이터 자산을 검색하면 일련의 전체 설명서를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05f44-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>

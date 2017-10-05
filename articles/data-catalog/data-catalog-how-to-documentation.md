---
title: "데이터 원본을 문서화하는 방법 | Microsoft Docs"
description: "Azure Data Catalog에서 데이터 자산을 문서화하는 방법을 강조 표시한 방법 문서입니다."
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
ms.openlocfilehash: ffe951f60afb57524568fe1ed3b3668d0088e124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="5cd5a-103">데이터 원본 문서화</span><span class="sxs-lookup"><span data-stu-id="5cd5a-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="5cd5a-104">소개</span><span class="sxs-lookup"><span data-stu-id="5cd5a-104">Introduction</span></span>
<span data-ttu-id="5cd5a-105">**Microsoft Azure 데이터 카탈로그** 는 등록 시스템 및 기업 데이터 원본을 위한 검색 시스템 역할을 하는 완전히 관리되는 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="5cd5a-106">다시 말해서 **Azure Data Catalog** 는 사람들이 데이터 원본을 검색하고 *이해*하고 사용하도록 하면서 조직의 기존 데이터로부터 더 많은 가치를 얻어내도록 돕는 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations to get more value from their existing data.</span></span>

<span data-ttu-id="5cd5a-107">**Azure Data Catalog**를 사용하여 데이터 원본을 등록하면 해당 메타데이터를 복사하고 서비스로 인덱싱하지만 여기서 끝이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span> <span data-ttu-id="5cd5a-108">**Azure Data Catalog** 를 사용하면 사용자에게 데이터 원본에 대한 사용 현황 및 일반적인 시나리오를 설명할 수 있는 고유한 전체 설명서를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-108">**Azure Data Catalog** also allows users to provide their own complete documentation that can describe the usage and common scenarios for the data source.</span></span>

<span data-ttu-id="5cd5a-109">[데이터 원본에 주석을 추가하는 방법](data-catalog-how-to-annotate.md)에서는 데이터 원본에 익숙한 전문가가 태그와 설명이 있는 주석을 추가할 수 있다는 점을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-109">In [How to annotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know the data source can annotate it with tags and a description.</span></span> <span data-ttu-id="5cd5a-110">**Azure Data Catalog** 포털은 사용자가 데이터 자산 및 컨테이너를 완벽하게 문서화할 수 있도록 다양한 텍스트 편집기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-110">The **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="5cd5a-111">편집기에는 제목, 텍스트 서식, 글머리 기호 목록, 번호 매기기 목록 및 테이블 등 단락 서식이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-111">The editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="5cd5a-112">태그와 설명은 간단한 주석에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="5cd5a-113">그러나 데이터 원본의 사용, 데이터 원본에 대한 비즈니스 시나리오를 더 잘 이해하도록 데이터 소비자를 돕기 위해 전문가는 자세한 전체 설명서를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-113">However, to help data consumers better understand the use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="5cd5a-114">데이터 원본을 문서화하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-114">It's easy to document a data source.</span></span> <span data-ttu-id="5cd5a-115">데이터 자산 또는 컨테이너를 선택하고 **설명서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="5cd5a-116">데이터 자산 문서화</span><span class="sxs-lookup"><span data-stu-id="5cd5a-116">Documenting data assets</span></span>
<span data-ttu-id="5cd5a-117">**Azure Data Catalog** 설명서를 사용하는 장점은 데이터 카탈로그를 콘텐츠 리포지토리로 사용하여 데이터 자산의 전체 설명을 만들 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-117">The benefit of **Azure Data Catalog** documentation allows you to use your Data Catalog as a content repository to create a complete narrative of your data assets.</span></span> <span data-ttu-id="5cd5a-118">컨테이너 및 테이블을 설명하는 자세한 내용을 둘러볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="5cd5a-119">SharePoint 또는 파일 공유 등의 다른 콘텐츠 리포지토리의 내용이 이미 있는 경우 이 기존 콘텐츠를 참조하는 자산 설명서 링크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-119">If you already have content in another content repository, such as SharePoint or a file share, you can add to the asset documentation links to reference this existing content.</span></span> <span data-ttu-id="5cd5a-120">이 기능을 사용해 기존 문서를 더 쉽게 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="5cd5a-121">설명서는 검색 인덱스에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="5cd5a-122">설명서의 수준은 데이터 자산 컨테이너의 특성 및 값을 설명하는 정도에서 컨테이너 내의 테이블 스키마에 대한 자세한 설명의 범위까지 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-122">The level of documentation can range from describing the characteristics and value of a data asset container to a detailed description of table schema within a container.</span></span> <span data-ttu-id="5cd5a-123">제공된 설명서의 수준은 비즈니스 요구 사항에 따라 결정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-123">The level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="5cd5a-124">하지만 데이터 자산을 문서화하는 일반적인 몇 가지 장단점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="5cd5a-125">컨테이너만 문서화: 모든 콘텐츠가 한 곳에 있지만 사용자가 필요한 정보를 결정하기 위해 필요한 세부 정보는 부족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-125">Document just a container: All the content is in one place, but might lack necessary details for users to make an informed decision.</span></span>
* <span data-ttu-id="5cd5a-126">테이블만 문서화: 콘텐츠는 해당 개체에 지정되지만 사용자가 문서를 여러 위치에서 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-126">Document just the tables: Content is specific to that object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="5cd5a-127">컨테이너 및 테이블 문서화: 가장 포괄적인 접근 방식이지만 문서의 유지 관리가 더 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of the documents.</span></span>

## <a name="summary"></a><span data-ttu-id="5cd5a-128">요약</span><span class="sxs-lookup"><span data-stu-id="5cd5a-128">Summary</span></span>
<span data-ttu-id="5cd5a-129">**Azure Data Catalog** 로 데이터 원본을 문서화하는 작업은 필요한 만큼의 세부 정보로 데이터 자산에 대한 설명을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="5cd5a-130">링크를 사용하여 기존 문서 및 데이터 자산을 함께 제공하는 기존 콘텐츠 리포지토리에 저장된 콘텐츠에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-130">By using links, you can link to content stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="5cd5a-131">사용자가 적절한 데이터 자산을 검색하면 일련의 전체 설명서를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd5a-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>

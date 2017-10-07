---
title: "Azure Data Catalog에 관리 분류 용 hello 비즈니스 용어집을 aaaSet | Microsoft Docs"
description: "방법 tooarticle 강조 hello 비즈니스 용어집을 정의 하 고 일반적인 비즈니스 어휘 tootag를 사용 하 여 Azure Data Catalog에 등록 된 데이터 자산입니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: c9adf663bd08ac3c0c7b5d3551e6af409fe69ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-business-glossary-for-governed-tagging"></a><span data-ttu-id="1f9be-103">태그 지정을 제어에 대 한 hello 비즈니스 용어집를 활용 설정</span><span class="sxs-lookup"><span data-stu-id="1f9be-103">Set up hello business glossary for governed tagging</span></span>
## <a name="introduction"></a><span data-ttu-id="1f9be-104">소개</span><span class="sxs-lookup"><span data-stu-id="1f9be-104">Introduction</span></span>
<span data-ttu-id="1f9be-105">Azure Data Catalog 쉽게 검색 하 고 이해 hello 데이터 소스 tooperform 분석 필요 하 고 결정을 내릴 수 있도록 데이터 원본 검색을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-105">Azure Data Catalog enables data-source discovery, so you can easily discover and understand hello data sources that you need tooperform analysis and make decisions.</span></span> <span data-ttu-id="1f9be-106">이러한 기능을 찾아 hello 광범위 한 사용 가능한 데이터 소스를 이해 하는 경우 hello 가장 큰 영향을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-106">These capabilities make hello biggest impact when you can find and understand hello broadest range of available data sources.</span></span>

<span data-ttu-id="1f9be-107">자산 데이터에 대한 이해를 크게 증진하는 데이터 카탈로그의 한 가지 기능이 태그 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-107">One Data Catalog feature that promotes greater understanding of assets data is tagging.</span></span> <span data-ttu-id="1f9be-108">태그를 사용 하 여 키워드 자산 또는 차례로 하므로 검색 또는 탐색을 통해 보다 쉽게 toodiscover hello 자산은 열과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-108">By using tagging, you can associate keywords with an asset or a column, which in turn makes it easier toodiscover hello asset via searching or browsing.</span></span> <span data-ttu-id="1f9be-109">또한 태그를 지정 하면 hello 컨텍스트와 hello asset의 의도 쉽게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-109">Tagging also helps you more easily understand hello context and intent of hello asset.</span></span>

<span data-ttu-id="1f9be-110">하지만 태그 지정이 자체적으로 문제를 유발하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-110">However, tagging can sometimes cause problems of its own.</span></span> <span data-ttu-id="1f9be-111">태그 지정을 통해 발생할 수 있는 문제의 예:</span><span class="sxs-lookup"><span data-stu-id="1f9be-111">Some examples of problems that tagging can introduce are:</span></span>

* <span data-ttu-id="1f9be-112">hello 일부 자산에 대 한 약어 및 다른 사용자에 확장 된 텍스트를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-112">hello use of abbreviations on some assets and expanded text on others.</span></span> <span data-ttu-id="1f9be-113">이러한 불일치는에 방해가 됩니다 한 자산 hello 검색 되었지만 hello 의도 hello 사용 하 여 tootag hello 자산 같은 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-113">This inconsistency hinders hello discovery of assets, even though hello intent was tootag hello assets with hello same tag.</span></span>
* <span data-ttu-id="1f9be-114">의미의 잠재적 변형은 컨텍스트에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-114">Potential variations in meaning, depending on context.</span></span> <span data-ttu-id="1f9be-115">예를 들어 태그 라는 *수익* 고객 데이터 집합 고객이 수익 의미 의미 하는 hello 분기별 판매 데이터 집합에 동일한 태그 수 hello 회사에 대 한 분기별 수익입니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-115">For example, a tag called *Revenue* on a customer data set might mean revenue by customer, but hello same tag on a quarterly sales dataset might mean quarterly revenue for hello company.</span></span>  

<span data-ttu-id="1f9be-116">toohelp 이러한 오류 코드 및 다른 유사한 문제 해결, 데이터 카탈로그 포함 비즈니스 용어집를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-116">toohelp address these and other similar challenges, Data Catalog includes a business glossary.</span></span>

<span data-ttu-id="1f9be-117">Hello 데이터 카탈로그 비즈니스 용어집을 사용 하 여 조직 주요 비즈니스 용어 및 해당 정의 toocreate 공통적인 비즈니스 용어 모음을 문서화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-117">By using hello Data Catalog business glossary, an organization can document key business terms and their definitions toocreate a common business vocabulary.</span></span> <span data-ttu-id="1f9be-118">이 거 버 넌이 스 hello 조직에서 사용 현황 데이터의에서 일관성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-118">This governance enables consistency in data usage across hello organization.</span></span> <span data-ttu-id="1f9be-119">지정 하는 단어 hello 비즈니스 용어집를 활용에 정의 된 후 tooa 데이터 자산 hello 카탈로그에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-119">After a term is defined in hello business glossary, it can be assigned tooa data asset in hello catalog.</span></span> <span data-ttu-id="1f9be-120">이 방법은 *태그 지정을 제어*는 hello와 동일한 방식으로 태그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-120">This approach, *governed tagging*, is hello same approach as tagging.</span></span>

## <a name="glossary-availability-and-privileges"></a><span data-ttu-id="1f9be-121">용어집 가용성 및 권한</span><span class="sxs-lookup"><span data-stu-id="1f9be-121">Glossary availability and privileges</span></span>
<span data-ttu-id="1f9be-122">hello 비즈니스 용어집를 활용 hello 표준 버전의 Azure Data Catalog만 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-122">hello business glossary is available only in hello Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="1f9be-123">hello 데이터 카탈로그의 무료 버전이 용어집을 보려면 없으며 관리 태그에 대 한 기능을 제공 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-123">hello Free Edition of Data Catalog does not include a glossary, and it does not provide capabilities for governed tagging.</span></span>

<span data-ttu-id="1f9be-124">Hello 비즈니스 용어집를 활용 hello 통해 액세스할 수 있습니다 **용어집** hello Data Catalog 포털 탐색 메뉴에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-124">You can access hello business glossary via hello **Glossary** option in hello Data Catalog portal's navigation menu.</span></span>  

![Hello 비즈니스 용어집를 활용에 액세스](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

<span data-ttu-id="1f9be-126">Hello 용어집 만들 수 있는 관리자 역할의 구성원과 데이터 카탈로그 관리자 편집 및 hello 비즈니스 용어집를 활용에 용어집 용어를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-126">Data Catalog administrators and members of hello glossary administrators role can create, edit, and delete glossary terms in hello business glossary.</span></span> <span data-ttu-id="1f9be-127">모든 데이터 카탈로그 사용자 hello 용어 정 및 용어집 용어를 사용 하 여 태그 자산 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-127">All Data Catalog users can view hello term definitions and tag assets with glossary terms.</span></span>

![새 용어 추가](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a><span data-ttu-id="1f9be-129">용어 만들기</span><span class="sxs-lookup"><span data-stu-id="1f9be-129">Creating glossary terms</span></span>
<span data-ttu-id="1f9be-130">데이터 카탈로그 관리자와 용어집 관리자 hello를 클릭 하 여 용어집 용어를 만들 수 **새 용어** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-130">Data Catalog administrators and glossary administrators can create glossary terms by clicking hello **New Term** button.</span></span> <span data-ttu-id="1f9be-131">각 용어집 용어 hello를 다음 필드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-131">Each glossary term contains hello following fields:</span></span>

* <span data-ttu-id="1f9be-132">Hello 용어에 대 한 비즈니스 정의</span><span class="sxs-lookup"><span data-stu-id="1f9be-132">A business definition for hello term</span></span>
* <span data-ttu-id="1f9be-133">Hello 자산 또는 열에 대 한 의도 한 hello 또는 비즈니스 규칙을 캡처하는 설명</span><span class="sxs-lookup"><span data-stu-id="1f9be-133">A description that captures hello intended use or business rules for hello asset or column</span></span>
* <span data-ttu-id="1f9be-134">Hello 용어에 대 한 가장 hello 아는 이해 관계자의 목록</span><span class="sxs-lookup"><span data-stu-id="1f9be-134">A list of stakeholders who know hello most about hello term</span></span>
* <span data-ttu-id="1f9be-135">hello 용어는 구성 하는 hello 계층 구조를 정의 하는 hello 상위 용어</span><span class="sxs-lookup"><span data-stu-id="1f9be-135">hello parent term, which defines hello hierarchy in which hello term is organized</span></span>

## <a name="glossary-term-hierarchies"></a><span data-ttu-id="1f9be-136">용어 계층 구조</span><span class="sxs-lookup"><span data-stu-id="1f9be-136">Glossary term hierarchies</span></span>
<span data-ttu-id="1f9be-137">Hello 데이터 카탈로그 비즈니스 용어집을 사용 하 여 조직 용어에 대 한 계층 구조와 해당 비즈니스 용어 모음을 설명할 수 및 해당 비즈니스 분류를 보다 잘 나타내는 용어의 분류를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-137">By using hello Data Catalog business glossary, an organization can describe its business vocabulary as a hierarchy of terms, and it can create a classification of terms that better represents its business taxonomy.</span></span>

<span data-ttu-id="1f9be-138">용어는 지정된 수준의 계층 구조에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-138">A term must be unique at a given level of hierarchy.</span></span> <span data-ttu-id="1f9be-139">중복 이름은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-139">Duplicate names are not allowed.</span></span> <span data-ttu-id="1f9be-140">계층의 수준 수 없는 제한 toohello는 없지만 계층은 종종 보다 쉽게 이해할 수 있는 세 가지 수준 이하의 경우.</span><span class="sxs-lookup"><span data-stu-id="1f9be-140">There is no limit toohello number of levels in a hierarchy, but a hierarchy is often more easily understood when there are three levels or fewer.</span></span>

<span data-ttu-id="1f9be-141">계층에서 hello 비즈니스 용어집를 활용 hello 사용은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-141">hello use of hierarchies in hello business glossary is optional.</span></span> <span data-ttu-id="1f9be-142">종료 hello 상위 용어 필드 용어집 용어에 대 한 빈 hello 용어집에서 용어 단순 (비 계층적) 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-142">Leaving hello parent term field blank for glossary terms creates a flat (non-hierarchical) list of terms in hello glossary.</span></span>  

## <a name="tagging-assets-with-glossary-terms"></a><span data-ttu-id="1f9be-143">용어를 사용하여 자산에 태그 지정</span><span class="sxs-lookup"><span data-stu-id="1f9be-143">Tagging assets with glossary terms</span></span>
<span data-ttu-id="1f9be-144">Hello 카탈로그 내에서 용어집 용어를 정의한 후 hello 자산 태그 지정의 환경은 최적화 toosearch hello 용어집으로 태그를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-144">After glossary terms have been defined within hello catalog, hello experience of tagging assets is optimized toosearch hello glossary as a user types a tag.</span></span> <span data-ttu-id="1f9be-145">hello Data Catalog 포털에서 일치 하는 용어집 용어 toochoose 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-145">hello Data Catalog portal displays a list of matching glossary terms toochoose from.</span></span> <span data-ttu-id="1f9be-146">용어집 용어 hello 목록에서 선택 하는 hello 사용자, hello 용어 toohello 자산 태그 (용어집 태그 라고도 함)으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-146">If hello user selects a glossary term from hello list, hello term is added toohello asset as a tag (also called a glossary tag).</span></span> <span data-ttu-id="1f9be-147">hello 사용자 선택할 수도 toocreate 새 태그 hello에 없는 단어를 입력 하 여 용어 설명 (사용자 정의 태그 라고도 함).</span><span class="sxs-lookup"><span data-stu-id="1f9be-147">hello user can also choose toocreate a new tag by typing a term that's not in hello glossary (also called a user tag).</span></span>

![사용자 태그 하나와 용어집 태그 두 개가 지정된 데이터 자산](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> <span data-ttu-id="1f9be-149">지원 되는 태그의 형식을 hello 데이터 카탈로그의 무료 버전에만 사용자 태그는 hello를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-149">User tags are hello only type of tag supported in hello Free Edition of Data Catalog.</span></span>
>
>

### <a name="hover-behavior-on-tags"></a><span data-ttu-id="1f9be-150">태그 가리키기 동작</span><span class="sxs-lookup"><span data-stu-id="1f9be-150">Hover behavior on tags</span></span>
<span data-ttu-id="1f9be-151">Hello Data Catalog 포털 hello 두 가지 유형의 태그는 시각적으로 고유 하 고 있는 다른 가리키기 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-151">In hello Data Catalog portal, hello two types of tags are visually distinct and present different hover behaviors.</span></span> <span data-ttu-id="1f9be-152">사용자 정의 태그를 마우스로 가리키면 hello 태그 텍스트 및 hello 사용자 또는 hello 태그 추가 사용자를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-152">When you hover over a user tag, you can see hello tag text and hello user or users who have added hello tag.</span></span> <span data-ttu-id="1f9be-153">용어집 태그를 마우스로 가리키면 hello 용어집 용어의 hello 정 및 링크 tooopen hello 비즈니스 용어집 tooview hello 전체 정의 hello 용어의 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-153">When you hover over a glossary tag, you also see hello definition of hello glossary term and a link tooopen hello business glossary tooview hello full definition of hello term.</span></span>

### <a name="search-filters-for-tags"></a><span data-ttu-id="1f9be-154">태그에 대한 검색 필터</span><span class="sxs-lookup"><span data-stu-id="1f9be-154">Search filters for tags</span></span>
<span data-ttu-id="1f9be-155">용어집 태그와 사용자 태그 모두 검색이 가능하며, 검색에 필터로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-155">Glossary tags and user tags are both searchable, and you can apply them as filters in a search.</span></span>

## <a name="summary"></a><span data-ttu-id="1f9be-156">요약</span><span class="sxs-lookup"><span data-stu-id="1f9be-156">Summary</span></span>
<span data-ttu-id="1f9be-157">Azure Data Catalog 및 hello 적용 하면 태그 지정의 hello 비즈니스 용어집을 사용 하 여 식별, 관리 및 데이터 자산 일관 된 방식으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-157">By using hello business glossary in Azure Data Catalog, and hello governed tagging it enables, you can identify, manage, and discover data assets in a consistent manner.</span></span> <span data-ttu-id="1f9be-158">hello 비즈니스 용어집를 활용 학습 조직 구성원이 hello 비즈니스 용어 모음을 승격할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-158">hello business glossary can promote learning of hello business vocabulary by organization members.</span></span> <span data-ttu-id="1f9be-159">hello 용어집 자산 검색 및 이해를 손쉽게 있는 의미 있는 메타 데이터를 캡처를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f9be-159">hello glossary also supports capturing meaningful metadata, which simplifies asset discovery and understanding.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f9be-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f9be-160">Next steps</span></span>
* [<span data-ttu-id="1f9be-161">비즈니스 용어집 작업에 대한 REST API 설명서</span><span class="sxs-lookup"><span data-stu-id="1f9be-161">REST API documentation for business glossary operations</span></span>](https://msdn.microsoft.com/library/mt708855.aspx)

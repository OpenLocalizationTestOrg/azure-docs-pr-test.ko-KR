---
title: "Azure Data Catalog에서 관리 태그 지정을 위한 비즈니스 용어집 설정 | Microsoft Docs"
description: "Azure Data Catalog의 비즈니스 용어집에서 일반적인 비즈니스 어휘를 정의하고 등록된 데이터 자산에 태그를 지정하는 데 사용하는 방법을 안내하는 문서."
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
ms.openlocfilehash: 83ca3b2d89a335a5fd6dddeaca7c11f6d0492234
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-the-business-glossary-for-governed-tagging"></a><span data-ttu-id="95eba-103">관리 태그 지정을 위한 비즈니스 용어집 설정</span><span class="sxs-lookup"><span data-stu-id="95eba-103">Set up the business glossary for governed tagging</span></span>
## <a name="introduction"></a><span data-ttu-id="95eba-104">소개</span><span class="sxs-lookup"><span data-stu-id="95eba-104">Introduction</span></span>
<span data-ttu-id="95eba-105">Azure Data Catalog는 데이터 원본 검색을 제공하여 사용자가 분석을 수행하고 결정을 내리는 데 필요한 데이터 원본을 쉽게 검색하고 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-105">Azure Data Catalog enables data-source discovery, so you can easily discover and understand the data sources that you need to perform analysis and make decisions.</span></span> <span data-ttu-id="95eba-106">이러한 기능은 사용자가 가장 넓은 범위의 사용 가능한 데이터 원본을 이해하고 찾을 수 있는 경우 엄청난 영향을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-106">These capabilities make the biggest impact when you can find and understand the broadest range of available data sources.</span></span>

<span data-ttu-id="95eba-107">자산 데이터에 대한 이해를 크게 증진하는 데이터 카탈로그의 한 가지 기능이 태그 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-107">One Data Catalog feature that promotes greater understanding of assets data is tagging.</span></span> <span data-ttu-id="95eba-108">태그 지정을 사용하여 검색을 통해 자산을 쉽게 검색할 수 있도록 하는 키워드를 자산 또는 열과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-108">By using tagging, you can associate keywords with an asset or a column, which in turn makes it easier to discover the asset via searching or browsing.</span></span> <span data-ttu-id="95eba-109">또한 태그를 지정하면 컨텍스트 및 자산의 의도를 쉽게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-109">Tagging also helps you more easily understand the context and intent of the asset.</span></span>

<span data-ttu-id="95eba-110">하지만 태그 지정이 자체적으로 문제를 유발하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-110">However, tagging can sometimes cause problems of its own.</span></span> <span data-ttu-id="95eba-111">태그 지정을 통해 발생할 수 있는 문제의 예:</span><span class="sxs-lookup"><span data-stu-id="95eba-111">Some examples of problems that tagging can introduce are:</span></span>

* <span data-ttu-id="95eba-112">일부 자산에 대해서는 약어를 사용하고 다른 자산에는 확장된 텍스트를 사용하는 경우.</span><span class="sxs-lookup"><span data-stu-id="95eba-112">The use of abbreviations on some assets and expanded text on others.</span></span> <span data-ttu-id="95eba-113">자산에 동일한 태그를 지정하는 것이 목적이긴 하지만, 이렇게 비일관적으로 작업하면 자산을 검색하는데 방해가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-113">This inconsistency hinders the discovery of assets, even though the intent was to tag the assets with the same tag.</span></span>
* <span data-ttu-id="95eba-114">의미의 잠재적 변형은 컨텍스트에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-114">Potential variations in meaning, depending on context.</span></span> <span data-ttu-id="95eba-115">예를 들어, 고객 데이터 집합의 *Revenue*라는 태그는 고객별 매출을 의미하지만, 분기별 판매 데이터 집합에서는 회사의 분기별 수입을 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-115">For example, a tag called *Revenue* on a customer data set might mean revenue by customer, but the same tag on a quarterly sales dataset might mean quarterly revenue for the company.</span></span>  

<span data-ttu-id="95eba-116">이러한 문제 및 그 밖의 유사한 문제를 해결하기 위해, 데이터 카탈로그에 비즈니스 용어집이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-116">To help address these and other similar challenges, Data Catalog includes a business glossary.</span></span>

<span data-ttu-id="95eba-117">데이터 카탈로그 비즈니스 용어집을 사용하여 조직은 주요 비즈니스 용어와 그에 대한 정의를 문서화하여 일반적인 비즈니스 어휘를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-117">By using the Data Catalog business glossary, an organization can document key business terms and their definitions to create a common business vocabulary.</span></span> <span data-ttu-id="95eba-118">이러한 관리 방식은 조직 전체의 일관적인 데이터 사용을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-118">This governance enables consistency in data usage across the organization.</span></span> <span data-ttu-id="95eba-119">비즈니스 용어집에서 용어를 정의한 후 카탈로그의 데이터 자산에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-119">After a term is defined in the business glossary, it can be assigned to a data asset in the catalog.</span></span> <span data-ttu-id="95eba-120">이 방법, *관리 태그 지정*은 태그 지정과 동일한 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-120">This approach, *governed tagging*, is the same approach as tagging.</span></span>

## <a name="glossary-availability-and-privileges"></a><span data-ttu-id="95eba-121">용어집 가용성 및 권한</span><span class="sxs-lookup"><span data-stu-id="95eba-121">Glossary availability and privileges</span></span>
<span data-ttu-id="95eba-122">비즈니스 용어집은 Azure Data Catalog 표준 버전에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-122">The business glossary is available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="95eba-123">데이터 카탈로그의 무료 버전은 용어집을 포함하지 않으며 관리 태그 지정에 대한 기능을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-123">The Free Edition of Data Catalog does not include a glossary, and it does not provide capabilities for governed tagging.</span></span>

<span data-ttu-id="95eba-124">데이터 카탈로그 포털의 탐색 메뉴에서 **용어집** 옵션을 통해 비즈니스 용어집에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-124">You can access the business glossary via the **Glossary** option in the Data Catalog portal's navigation menu.</span></span>  

![비즈니스 용어집에 액세스](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

<span data-ttu-id="95eba-126">데이터 카탈로그 관리자 및 용어집 관리자 역할을 하는 멤버는 비즈니스 용어집에서 용어를 만들고, 편집하고, 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-126">Data Catalog administrators and members of the glossary administrators role can create, edit, and delete glossary terms in the business glossary.</span></span> <span data-ttu-id="95eba-127">모든 데이터 카탈로그 사용자는 용어 정의를 볼 수 있고, 용어를 사용하여 자산에 태그를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-127">All Data Catalog users can view the term definitions and tag assets with glossary terms.</span></span>

![새 용어 추가](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a><span data-ttu-id="95eba-129">용어 만들기</span><span class="sxs-lookup"><span data-stu-id="95eba-129">Creating glossary terms</span></span>
<span data-ttu-id="95eba-130">데이터 카탈로그 관리자 및 용어집 관리자는 **새 용어** 단추를 클릭하여 용어를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-130">Data Catalog administrators and glossary administrators can create glossary terms by clicking the **New Term** button.</span></span> <span data-ttu-id="95eba-131">각 용어는 다음 필드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-131">Each glossary term contains the following fields:</span></span>

* <span data-ttu-id="95eba-132">용어에 대한 비즈니스 정의</span><span class="sxs-lookup"><span data-stu-id="95eba-132">A business definition for the term</span></span>
* <span data-ttu-id="95eba-133">자산 또는 열에 대한 사용 목적 또는 비즈니스 규칙을 포함하는 설명</span><span class="sxs-lookup"><span data-stu-id="95eba-133">A description that captures the intended use or business rules for the asset or column</span></span>
* <span data-ttu-id="95eba-134">용어를 가장 잘 아는 관련자 목록</span><span class="sxs-lookup"><span data-stu-id="95eba-134">A list of stakeholders who know the most about the term</span></span>
* <span data-ttu-id="95eba-135">용어가 구성되는 계층 구조를 정의하는 상위 용어</span><span class="sxs-lookup"><span data-stu-id="95eba-135">The parent term, which defines the hierarchy in which the term is organized</span></span>

## <a name="glossary-term-hierarchies"></a><span data-ttu-id="95eba-136">용어 계층 구조</span><span class="sxs-lookup"><span data-stu-id="95eba-136">Glossary term hierarchies</span></span>
<span data-ttu-id="95eba-137">데이터 카탈로그 비즈니스 용어집을 사용하여 조직은 용어의 계층 구조로 해당 비즈니스 용어 모음을 설명하고 해당 비즈니스 분류를 보다 잘 나타내는 용어의 분류를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-137">By using the Data Catalog business glossary, an organization can describe its business vocabulary as a hierarchy of terms, and it can create a classification of terms that better represents its business taxonomy.</span></span>

<span data-ttu-id="95eba-138">용어는 지정된 수준의 계층 구조에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-138">A term must be unique at a given level of hierarchy.</span></span> <span data-ttu-id="95eba-139">중복 이름은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-139">Duplicate names are not allowed.</span></span> <span data-ttu-id="95eba-140">계층 구조 내 수준의 수에는 제한이 없지만, 계층 구조 내의 수준이 3개 이하인 경우에 보다 쉽게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-140">There is no limit to the number of levels in a hierarchy, but a hierarchy is often more easily understood when there are three levels or fewer.</span></span>

<span data-ttu-id="95eba-141">비즈니스 용어집에 계층 구조를 사용하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-141">The use of hierarchies in the business glossary is optional.</span></span> <span data-ttu-id="95eba-142">용어에 대한 상위 용어 필드를 비워두면 용어집 내에 단순(비계층적인) 용어 목록이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-142">Leaving the parent term field blank for glossary terms creates a flat (non-hierarchical) list of terms in the glossary.</span></span>  

## <a name="tagging-assets-with-glossary-terms"></a><span data-ttu-id="95eba-143">용어를 사용하여 자산에 태그 지정</span><span class="sxs-lookup"><span data-stu-id="95eba-143">Tagging assets with glossary terms</span></span>
<span data-ttu-id="95eba-144">카탈로그 내에 용어가 정의되고 나면, 자산에 태그를 지정하는 환경은 사용자가 태그를 입력하여 용어를 검색하도록 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-144">After glossary terms have been defined within the catalog, the experience of tagging assets is optimized to search the glossary as a user types a tag.</span></span> <span data-ttu-id="95eba-145">데이터 카탈로그 포털에 사용자가 선택할 수 있도록 일치하는 용어 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-145">The Data Catalog portal displays a list of matching glossary terms to choose from.</span></span> <span data-ttu-id="95eba-146">사용자가 목록에서 용어를 선택하면, 용어는 자산에 태그로 추가됩니다(용어집 태그라고도 함).</span><span class="sxs-lookup"><span data-stu-id="95eba-146">If the user selects a glossary term from the list, the term is added to the asset as a tag (also called a glossary tag).</span></span> <span data-ttu-id="95eba-147">사용자는 용어집에 없는 용어를 입력하여 새 태그를 만들 수도 있습니다(사용자 태그라고도 함).</span><span class="sxs-lookup"><span data-stu-id="95eba-147">The user can also choose to create a new tag by typing a term that's not in the glossary (also called a user tag).</span></span>

![사용자 태그 하나와 용어집 태그 두 개가 지정된 데이터 자산](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> <span data-ttu-id="95eba-149">사용자 태그는 데이터 카탈로그 무료 버전에서 유일하게 지원되는 태그 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-149">User tags are the only type of tag supported in the Free Edition of Data Catalog.</span></span>
>
>

### <a name="hover-behavior-on-tags"></a><span data-ttu-id="95eba-150">태그 가리키기 동작</span><span class="sxs-lookup"><span data-stu-id="95eba-150">Hover behavior on tags</span></span>
<span data-ttu-id="95eba-151">데이터 카탈로그 포털에서, 두 가지 유형의 태그는 시각적으로 구분되며 서로 다른 가리키기 동작을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-151">In the Data Catalog portal, the two types of tags are visually distinct and present different hover behaviors.</span></span> <span data-ttu-id="95eba-152">사용자 태그를 가리키면 태그 텍스트와 태그를 추가한 사용자(한 명 또는 여러 명)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-152">When you hover over a user tag, you can see the tag text and the user or users who have added the tag.</span></span> <span data-ttu-id="95eba-153">용어집 태그를 가리키면, 용어에 대한 정의와 링크(비즈니스 용어집을 열어서 용어에 대한 전체 정의를 표시하는)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-153">When you hover over a glossary tag, you also see the definition of the glossary term and a link to open the business glossary to view the full definition of the term.</span></span>

### <a name="search-filters-for-tags"></a><span data-ttu-id="95eba-154">태그에 대한 검색 필터</span><span class="sxs-lookup"><span data-stu-id="95eba-154">Search filters for tags</span></span>
<span data-ttu-id="95eba-155">용어집 태그와 사용자 태그 모두 검색이 가능하며, 검색에 필터로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-155">Glossary tags and user tags are both searchable, and you can apply them as filters in a search.</span></span>

## <a name="summary"></a><span data-ttu-id="95eba-156">요약</span><span class="sxs-lookup"><span data-stu-id="95eba-156">Summary</span></span>
<span data-ttu-id="95eba-157">Azure Data Catalog의 비즈니스 용어집과 여기에서 사용할 수 있는 관리 태그 지정을 사용하면, 일관된 방식으로 데이터 자산을 식별, 관리, 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-157">By using the business glossary in Azure Data Catalog, and the governed tagging it enables, you can identify, manage, and discover data assets in a consistent manner.</span></span> <span data-ttu-id="95eba-158">비즈니스 용어집은 조직 구성원에 의해 비즈니스 용어 모음의 활용을 승격할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-158">The business glossary can promote learning of the business vocabulary by organization members.</span></span> <span data-ttu-id="95eba-159">또한 용어집은 자산 검색 및 이해를 간소화하는 의미 있는 메타데이터 캡처를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="95eba-159">The glossary also supports capturing meaningful metadata, which simplifies asset discovery and understanding.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95eba-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95eba-160">Next steps</span></span>
* [<span data-ttu-id="95eba-161">비즈니스 용어집 작업에 대한 REST API 설명서</span><span class="sxs-lookup"><span data-stu-id="95eba-161">REST API documentation for business glossary operations</span></span>](https://msdn.microsoft.com/library/mt708855.aspx)

---
title: "Azure Data Catalog에서 데이터 자산 aaaManage | Microsoft Docs"
description: "hello 문서 toocontrol 표시 유형 및 데이터 자산의 소유권 Azure Data Catalog에 등록 하는 방법을 강조 표시 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="7d96b-103">Azure Data Catalog에서 데이터 자산 관리</span><span class="sxs-lookup"><span data-stu-id="7d96b-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="7d96b-104">소개</span><span class="sxs-lookup"><span data-stu-id="7d96b-104">Introduction</span></span>
<span data-ttu-id="7d96b-105">Azure Data Catalog는 쉽게 검색 하 고 이해 hello 데이터 원본 tooperform 분석 필요 하 고 내릴 수 있도록 데이터 원본 검색을 위해 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand hello data sources you need tooperform analysis and make decisions.</span></span> <span data-ttu-id="7d96b-106">이러한 검색 기능 및 다른 사용자가 찾아 hello 광범위 한 사용 가능한 데이터 소스를 이해할 수 때 hello 가장 큰 영향을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-106">These discovery capabilities make hello biggest impact when you and other users can find and understand hello broadest range of available data sources.</span></span> <span data-ttu-id="7d96b-107">에 이러한 요소와 데이터 카탈로그의 hello 기본 동작은 모든 등록 된 데이터 원본 toobe 표시 tooand 검색 가능한 모든 카탈로그 사용자에 대 한입니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-107">With these elements in mind, hello default behavior of Data Catalog is for all registered data sources toobe visible tooand discoverable by all catalog users.</span></span>

<span data-ttu-id="7d96b-108">데이터 카탈로그 얻지 자체 toohello 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-108">Data Catalog does not give you access toohello data itself.</span></span> <span data-ttu-id="7d96b-109">데이터 액세스는 hello hello 데이터 원본 소유자에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-109">Data access is controlled by hello owner of hello data source.</span></span> <span data-ttu-id="7d96b-110">데이터 카탈로그와 데이터 소스를 검색 하 고 hello 카달로그에 등록 하는 관련된 toohello 원본 hello 메타 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-110">With Data Catalog, you can discover data sources and view hello metadata that's related toohello sources that are registered in hello catalog.</span></span>

<span data-ttu-id="7d96b-111">그러나 데이터 원본 표시 toospecific 사용자 또는 특정 그룹의 toomembers 수만 해야 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-111">There might be situations, however, where data sources should only be visible toospecific users, or toomembers of specific groups.</span></span> <span data-ttu-id="7d96b-112">이러한 시나리오에서는 사용자 hello 카탈로그 내에서 등록 된 데이터 자산의 소유권을 가져올 수 있습니다 및 다음 hello 자산을 소유한 hello 표시 여부를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-112">In such scenarios, users can take ownership of registered data assets within hello catalog and then control hello visibility of hello assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="7d96b-113">이 문서에 설명 된 hello 기능은 hello 표준 버전의 Azure Data Catalog에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-113">hello functionality described in this article is available only in hello Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="7d96b-114">hello 무료 버전을 제공 하지 않습니다 소유권 및 데이터 자산 가시성 제한에 대 한 기능.</span><span class="sxs-lookup"><span data-stu-id="7d96b-114">hello Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="7d96b-115">데이터 자산의 소유권 관리</span><span class="sxs-lookup"><span data-stu-id="7d96b-115">Manage ownership of data assets</span></span>
<span data-ttu-id="7d96b-116">기본적으로 데이터 카탈로그에 등록된 데이터 자산은 소유되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="7d96b-117">권한 tooaccess hello 카탈로그에 있는 모든 사용자 검색 하 고 이러한 자산에 주석을 달 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-117">Any user with permission tooaccess hello catalog can discover and annotate these assets.</span></span> <span data-ttu-id="7d96b-118">사용자가 소유 하지 않은 데이터 자산의 소유권을 가져올 다음 hello 자산을 소유한 hello 가시성 제한 수 있으며</span><span class="sxs-lookup"><span data-stu-id="7d96b-118">Users can take ownership of unowned data assets and then limit hello visibility of hello assets they own.</span></span>

<span data-ttu-id="7d96b-119">데이터 카탈로그에서 데이터 자산을 소유 하 고 hello 소유자가 권한이 있는 사용자만는 hello 자산을 검색 하 고 해당 메타 데이터를 볼 수 및 hello 소유자만 hello 카탈로그에서 hello 자산을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-119">When a data asset in Data Catalog is owned, only users who are authorized by hello owners can discover hello asset and view its metadata, and only hello owners can delete hello asset from hello catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="7d96b-120">데이터 카탈로그에 소유권 hello 카탈로그에 저장 된 hello 메타를 데이터만 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-120">Ownership in Data Catalog affects only hello metadata that's stored in hello catalog.</span></span> <span data-ttu-id="7d96b-121">소유권은 hello 데이터 원본에 대 한 모든 권한을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-121">Ownership does not confer any permissions on hello underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="7d96b-122">소유권 가져오기</span><span class="sxs-lookup"><span data-stu-id="7d96b-122">Take ownership</span></span>
<span data-ttu-id="7d96b-123">Hello를 선택 하 여 데이터 자산의 소유권을 가져올 수 사용자 **Take Ownership** hello Data Catalog 포털에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-123">Users can take ownership of data assets by selecting hello **Take Ownership** option in hello Data Catalog portal.</span></span> <span data-ttu-id="7d96b-124">특별 권한은 없습니다 소유 되지 않은 데이터 자산의 필요한 tootake 소유권을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-124">No special permissions are required tootake ownership of an unowned data asset.</span></span> <span data-ttu-id="7d96b-125">모든 사용자는 소유되지 않은 데이터 자산을 소유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="7d96b-126">소유자 및 공동 소유자 추가</span><span class="sxs-lookup"><span data-stu-id="7d96b-126">Add owners and co-owners</span></span>
<span data-ttu-id="7d96b-127">데이터 자산이 이미 소유된 경우 다른 사용자는 소유권을 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="7d96b-128">기존 소유자에 의해 공동 소유자로 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="7d96b-129">소유자는 추가 사용자 또는 보안 그룹을 공동 소유자로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="7d96b-130">이 모든 소유한 데이터 자산에 대 한 모범 사례 toohave 소유자로 두 개 이상의 개인은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-130">It is a best practice toohave at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="7d96b-131">소유자 제거</span><span class="sxs-lookup"><span data-stu-id="7d96b-131">Remove owners</span></span>
<span data-ttu-id="7d96b-132">자산 소유자가 공동 소유자를 추가할 수 있는 것처럼 자산 소유자는 공동 소유자를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="7d96b-133">소유자로 본인을 제거 하는 자산 소유자 hello 자산을 관리할 더 이상 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-133">An asset owner who removes him or herself as an owner can no longer manage hello asset.</span></span> <span data-ttu-id="7d96b-134">Hello 자산 소유자 소유자로 본인 제거 되 고 다른 없습니다 공동 소유자는, hello 자산 상태 소유 tooan로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-134">If hello asset owner removes him or herself as an owner and there are no other co-owners, hello asset reverts tooan unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="7d96b-135">컨트롤 표시 여부</span><span class="sxs-lookup"><span data-stu-id="7d96b-135">Control visibility</span></span>
<span data-ttu-id="7d96b-136">데이터 자산 소유자는 자신이 소유한 hello 데이터 자산의 hello 표시 유형을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-136">Data-asset owners can control hello visibility of hello data assets they own.</span></span> <span data-ttu-id="7d96b-137">hello 기본값으로 toorestrict 표시 유형, 모든 사용자를 검색할 수는 데이터 카탈로그 및 보기 hello 데이터 자산 여기서 hello 자산 소유자 설정/해제할 수에서 hello 표시 유형 설정이 **Everyone** 너무**소유자 및 이러한 사용자** hello 자산에 대 한 hello 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-137">toorestrict visibility as hello default, where all Data Catalog users can discover and view hello data asset, hello asset owner can toggle hello visibility setting from **Everyone** too**Owners & These Users** in hello properties for hello asset.</span></span> <span data-ttu-id="7d96b-138">그런 다음 소유자는 특정 사용자 및 보안 그룹을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="7d96b-139">가능 하면 항상 toosecurity 그룹 및 사용자가 tooindividual 아닌 자산 소유권 및 표시 유형 사용 권한 할당 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-139">Whenever possible, asset ownership and visibility permissions should be assigned toosecurity groups and not tooindividual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="7d96b-140">카탈로그 관리자</span><span class="sxs-lookup"><span data-stu-id="7d96b-140">Catalog administrators</span></span>
<span data-ttu-id="7d96b-141">데이터 카탈로그 관리자는 암시적으로 공동 소유자 hello 카탈로그에 있는 모든 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-141">Data Catalog administrators are implicitly co-owners of all assets in hello catalog.</span></span> <span data-ttu-id="7d96b-142">자산 소유자 관리자에 게 가시성을 제거할 수 없습니다 및 관리자 소유권과 hello 카탈로그에 있는 모든 데이터 자산에 대 한 표시 유형을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in hello catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="7d96b-143">요약</span><span class="sxs-lookup"><span data-stu-id="7d96b-143">Summary</span></span>
<span data-ttu-id="7d96b-144">모든 카탈로그 사용자 toocontribute 허용 하 고 검색 하는 hello 데이터 카탈로그 crowdsourcing 모델 toometadata 및 데이터 자산을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-144">hello Data Catalog crowdsourcing model toometadata and data asset discovery allows all catalog users toocontribute and discover.</span></span> <span data-ttu-id="7d96b-145">데이터 카탈로그의 Standard Edition hello 소유권 및 관리 toolimit hello 표시 유형 및 특정 데이터 자산 사용을 위해 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d96b-145">hello Standard Edition of Data Catalog is designed for ownership and management toolimit hello visibility and use of specific data assets.</span></span>

---
title: "Azure Data Catalog에서 데이터 자산 관리 | Microsoft Docs"
description: "문서는 Azure Data Catalog에 등록된 데이터 자산의 표시 여부 및 소유권을 제어하는 방법을 강조 표시합니다."
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
ms.openlocfilehash: 8b9159b7bc4f7b2dac12d9012c6c903e75a6ac16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="9229a-103">Azure Data Catalog에서 데이터 자산 관리</span><span class="sxs-lookup"><span data-stu-id="9229a-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="9229a-104">소개</span><span class="sxs-lookup"><span data-stu-id="9229a-104">Introduction</span></span>
<span data-ttu-id="9229a-105">Azure Data Catalog는 사용자가 분석을 수행하고 결정을 내리는 데 필요한 데이터 원본을 쉽게 검색하고 이해할 수 있도록 데이터 원본 검색을 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand the data sources you need to perform analysis and make decisions.</span></span> <span data-ttu-id="9229a-106">이러한 검색 기능은 모든 사용자가 가장 넓은 범위의 사용 가능한 데이터 원본을 이해하고 찾을 수 있는 경우 엄청난 영향을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-106">These discovery capabilities make the biggest impact when you and other users can find and understand the broadest range of available data sources.</span></span> <span data-ttu-id="9229a-107">이러한 요소를 고려하여 데이터 카탈로그의 기본 동작은 모든 등록된 데이터 원본을 모든 카탈로그 사용자에게 표시하며 검색할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-107">With these elements in mind, the default behavior of Data Catalog is for all registered data sources to be visible to and discoverable by all catalog users.</span></span>

<span data-ttu-id="9229a-108">데이터 카탈로그는 사용자가 데이터 자체에 액세스할 권한을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-108">Data Catalog does not give you access to the data itself.</span></span> <span data-ttu-id="9229a-109">데이터 원본의 소유자가 데이터 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-109">Data access is controlled by the owner of the data source.</span></span> <span data-ttu-id="9229a-110">데이터 카탈로그를 사용하면 데이터 원본을 검색하고 카탈로그에 등록된 원본과 관련된 메타데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-110">With Data Catalog, you can discover data sources and view the metadata that's related to the sources that are registered in the catalog.</span></span>

<span data-ttu-id="9229a-111">그러나 데이터 원본을 특정 사용자 또는 특정 그룹의 구성원에게만 표시해야 할 상황이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-111">There might be situations, however, where data sources should only be visible to specific users, or to members of specific groups.</span></span> <span data-ttu-id="9229a-112">이러한 시나리오에서 사용자는 카탈로그 내에서 등록된 데이터 자산의 소유권을 가져온 다음 소유한 자산의 표시 여부를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-112">In such scenarios, users can take ownership of registered data assets within the catalog and then control the visibility of the assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="9229a-113">이 문서에서 설명한 기능은 Azure Data Catalog의 표준 버전에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-113">The functionality described in this article is available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="9229a-114">무료 버전에서는 소유권 및 데이터 자산의 표시를 제한하기 위한 기능을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-114">The Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="9229a-115">데이터 자산의 소유권 관리</span><span class="sxs-lookup"><span data-stu-id="9229a-115">Manage ownership of data assets</span></span>
<span data-ttu-id="9229a-116">기본적으로 데이터 카탈로그에 등록된 데이터 자산은 소유되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="9229a-117">카탈로그에 액세스할 수 있는 권한을 가진 모든 사용자는 이러한 자산을 검색하고 주석을 달 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-117">Any user with permission to access the catalog can discover and annotate these assets.</span></span> <span data-ttu-id="9229a-118">사용자는 소유하지 않은 데이터 자산의 소유권을 가져올 수 있고 자신이 소유한 자산의 표시를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-118">Users can take ownership of unowned data assets and then limit the visibility of the assets they own.</span></span>

<span data-ttu-id="9229a-119">데이터 카탈로그의 데이터 자산을 소유하는 경우 소유자에게 권한을 부여받은 사용자만이 자산을 검색하고 해당 메타데이터를 볼 수 있으며 소유자만이 카탈로그에서 자산을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-119">When a data asset in Data Catalog is owned, only users who are authorized by the owners can discover the asset and view its metadata, and only the owners can delete the asset from the catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="9229a-120">데이터 카탈로그의 소유권은 카탈로그에 저장된 메타데이터에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-120">Ownership in Data Catalog affects only the metadata that's stored in the catalog.</span></span> <span data-ttu-id="9229a-121">소유권은 기본 데이터 원본에 대한 권한을 부여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-121">Ownership does not confer any permissions on the underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="9229a-122">소유권 가져오기</span><span class="sxs-lookup"><span data-stu-id="9229a-122">Take ownership</span></span>
<span data-ttu-id="9229a-123">사용자는 데이터 카탈로그 포털에서 **소유권 가져오기** 옵션을 선택하여 데이터 자산의 소유권을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-123">Users can take ownership of data assets by selecting the **Take Ownership** option in the Data Catalog portal.</span></span> <span data-ttu-id="9229a-124">소유되지 않은 데이터 자산의 소유권을 가져오는 데 특별한 권한이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-124">No special permissions are required to take ownership of an unowned data asset.</span></span> <span data-ttu-id="9229a-125">모든 사용자는 소유되지 않은 데이터 자산을 소유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="9229a-126">소유자 및 공동 소유자 추가</span><span class="sxs-lookup"><span data-stu-id="9229a-126">Add owners and co-owners</span></span>
<span data-ttu-id="9229a-127">데이터 자산이 이미 소유된 경우 다른 사용자는 소유권을 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="9229a-128">기존 소유자에 의해 공동 소유자로 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="9229a-129">소유자는 추가 사용자 또는 보안 그룹을 공동 소유자로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="9229a-130">소유한 데이터 자산에 둘 이상의 개인이 소유자인 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-130">It is a best practice to have at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="9229a-131">소유자 제거</span><span class="sxs-lookup"><span data-stu-id="9229a-131">Remove owners</span></span>
<span data-ttu-id="9229a-132">자산 소유자가 공동 소유자를 추가할 수 있는 것처럼 자산 소유자는 공동 소유자를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="9229a-133">자신을 소유자에서 제거하는 자산 소유자는 자산을 더 이상 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-133">An asset owner who removes him or herself as an owner can no longer manage the asset.</span></span> <span data-ttu-id="9229a-134">자산 소유자가 자신을 소유자에서 제거하고 다른 공동 소유자가 없는 경우 자산은 소유하지 않은 상태로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-134">If the asset owner removes him or herself as an owner and there are no other co-owners, the asset reverts to an unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="9229a-135">컨트롤 표시 여부</span><span class="sxs-lookup"><span data-stu-id="9229a-135">Control visibility</span></span>
<span data-ttu-id="9229a-136">데이터 자산 소유자는 자신이 소유한 데이터 자산의 표시 여부를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-136">Data-asset owners can control the visibility of the data assets they own.</span></span> <span data-ttu-id="9229a-137">모든 데이터 카탈로그 사용자가 데이터 자산을 검색하고 볼 수 있는 기본값에서 표시를 제한하려면 자산 소유자는 자산에 대한 속성에서 표시 여부 설정을 **모두**에서 **소유자 및 다음 사용자**로 설정/해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-137">To restrict visibility as the default, where all Data Catalog users can discover and view the data asset, the asset owner can toggle the visibility setting from **Everyone** to **Owners & These Users** in the properties for the asset.</span></span> <span data-ttu-id="9229a-138">그런 다음 소유자는 특정 사용자 및 보안 그룹을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="9229a-139">가능한 경우에는 개별 사용자가 아닌 보안 그룹에 자산 소유권 및 표시 여부 권한을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-139">Whenever possible, asset ownership and visibility permissions should be assigned to security groups and not to individual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="9229a-140">카탈로그 관리자</span><span class="sxs-lookup"><span data-stu-id="9229a-140">Catalog administrators</span></span>
<span data-ttu-id="9229a-141">데이터 카탈로그 관리자는 암시적으로 카탈로그에서 모든 자산의 공동 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-141">Data Catalog administrators are implicitly co-owners of all assets in the catalog.</span></span> <span data-ttu-id="9229a-142">자산 소유자는 관리자에게 표시되지 않도록 할 수 없고 관리자는 카탈로그의 모든 데이터 자산의 소유권 및 표시 여부를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in the catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="9229a-143">요약</span><span class="sxs-lookup"><span data-stu-id="9229a-143">Summary</span></span>
<span data-ttu-id="9229a-144">메타데이터 및 데이터 자산 검색에 대한 데이터 카탈로그의 크라우드소싱 모델을 사용하면 모든 카탈로그 사용자가 기여하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-144">The Data Catalog crowdsourcing model to metadata and data asset discovery allows all catalog users to contribute and discover.</span></span> <span data-ttu-id="9229a-145">데이터 카탈로그의 표준 버전은 특정 데이터 자산의 표시 및 사용을 제한하는 소유권 및 관리를 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9229a-145">The Standard Edition of Data Catalog is designed for ownership and management to limit the visibility and use of specific data assets.</span></span>

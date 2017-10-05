---
title: "Marketplace에서 Azure 관리되는 응용 프로그램 | Microsoft Docs"
description: "Marketplace를 통해 사용할 수 있는 Azure 관리되는 응용 프로그램에 대해 설명합니다."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 58ac7665abf7e75a43bb0b92bdf6f41005c3efe8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="00226-103">Marketplace에서 Azure 관리되는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="00226-103">Azure managed applications in the Marketplace</span></span>

 <span data-ttu-id="00226-104">MSP, ISV 및 SI(시스템 통합자)는 Azure 관리되는 응용 프로그램을 사용하여 모든 Azure Marketplace 고객에게 솔루션을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications to offer their solutions to all Azure Marketplace customers.</span></span> <span data-ttu-id="00226-105">이러한 솔루션으로 고객에 대한 유지 관리 및 서비스 오버헤드가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="00226-105">Such solutions reduce the maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="00226-106">게시자는 Marketplace를 통해 인프라 및 소프트웨어를 판매할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-106">Publishers can sell infrastructure and software through the Marketplace.</span></span> <span data-ttu-id="00226-107">서비스 및 작업 지원을 관리되는 응용 프로그램에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-107">They can attach services and operational support to managed applications.</span></span> <span data-ttu-id="00226-108">자세한 내용은 [관리되는 응용 프로그램 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00226-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="00226-109">이 문서에서는 MSP, ISV 또는 SI가 응용 프로그램을 Marketplace에 게시하고 고객에게 광범위하게 제공하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-109">This article explains how an MSP, ISV, or SI can publish an application to the Marketplace and make it broadly available to customers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="00226-110">관리되는 응용 프로그램을 게시하기 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="00226-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="00226-111">Marketplace에 등록하기 위한 필수 조건:</span><span class="sxs-lookup"><span data-stu-id="00226-111">Prerequisites to listing in the Marketplace:</span></span>

* <span data-ttu-id="00226-112">기술</span><span class="sxs-lookup"><span data-stu-id="00226-112">Technical</span></span>

    *  <span data-ttu-id="00226-113">Azure Resource Manager 템플릿의 기본 구조 및 구문에 대한 자세한 내용은 [Azure Resource Manager 템플릿](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00226-113">For information about the basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="00226-114">전체 템플릿 솔루션을 보려면 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/en-us/documentation/templates/) 또는 [빠른 시작 템플릿 리포지토리](https://github.com/azure/azure-quickstart-templates)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00226-114">To view complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or the [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="00226-115">Marketplace를 통해 응용 프로그램을 배포하는 고객을 위한 인터페이스를 만드는 방법에 대한 자세한 정보는 [사용자 인터페이스 정의 파일 만들기](managed-application-createuidefinition-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00226-115">For information about how to create the interface for customers who deploy your application through the Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="00226-116">비기술(비즈니스 요구 사항)</span><span class="sxs-lookup"><span data-stu-id="00226-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="00226-117">회사 또는 해당 자회사는 Marketplace에서 지원하는 판매처 국가에 위치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-117">Your company or its subsidiary must be located in a country where sales are supported by the Marketplace.</span></span>
    *   <span data-ttu-id="00226-118">제품은 Marketplace에서 지원하는 청구 모델과 호환되는 방식으로 허가를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-118">Your product must be licensed in a way that is compatible with billing models supported by the Marketplace.</span></span>
    *   <span data-ttu-id="00226-119">상업적이고 합리적인 방식으로 고객이 이용할 수 있는 기술 지원을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-119">You're responsible for making technical support available to customers in a commercially reasonable manner.</span></span> <span data-ttu-id="00226-120">이러한 지원은 평가판, 유료 또는 커뮤니티 지원을 통해 이루어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-120">The support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="00226-121">소프트웨어 및 타사 소프트웨어 종속성에 대해 사용 허가를 받을 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="00226-122">Marketplace 및 Azure Portal에 등록할 제품에 대한 기준을 충족하는 콘텐츠를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-122">You must provide content that meets criteria for your offering to be listed in the Marketplace and in the Azure portal.</span></span>
    *   <span data-ttu-id="00226-123">Azure Marketplace 참가 정책 및 게시자 약관의 조건에 동의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-123">You must agree to the terms of the Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="00226-124">사용 약관, Microsoft 개인정보처리방침 및 Microsoft Azure Certified 프로그램 계약을 준수한다는 데 동의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-124">You must agree to comply with the Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="00226-125">새 Azure 응용 프로그램 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="00226-125">Create a new Azure application offer</span></span>

<span data-ttu-id="00226-126">필수 구성 요소를 충족하면 관리되는 응용 프로그램 제품을 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-126">After you meet the prerequisites, you're ready to create your managed application offer.</span></span> <span data-ttu-id="00226-127">제품 및 SKU를 간략히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="00226-128">제안</span><span class="sxs-lookup"><span data-stu-id="00226-128">Offer</span></span>

<span data-ttu-id="00226-129">관리되는 응용 프로그램에 대한 제품은 게시자가 제공하는 제품의 클래스에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-129">The offer for a managed application corresponds to a class of product offering from a publisher.</span></span> <span data-ttu-id="00226-130">새로운 유형의 솔루션/응용 프로그램을 Marketplace에서 사용할 수 있도록 하려는 경우 새 제품으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-130">If you have a new type of solution/application that you want to make available in the Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="00226-131">제품은 SKU의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="00226-132">모든 제품은 Marketplace에 고유 엔터티로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="00226-132">Every offer appears as its own entity in the Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="00226-133">SKU</span><span class="sxs-lookup"><span data-stu-id="00226-133">SKU</span></span>

<span data-ttu-id="00226-134">SKU는 제품의 가장 작은 구매 가능 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-134">A SKU is the smallest purchasable unit of an offer.</span></span> <span data-ttu-id="00226-135">같은 제품 클래스(제품) 내에서 SKU를 사용하여 다음을 구별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-135">You can use a SKU within the same product class (offer) to differentiate between:</span></span>

* <span data-ttu-id="00226-136">제공되는 다양한 기능.</span><span class="sxs-lookup"><span data-stu-id="00226-136">Different features that are supported.</span></span>
* <span data-ttu-id="00226-137">제품이 관리되는지 관리되지 않는지 여부.</span><span class="sxs-lookup"><span data-stu-id="00226-137">Whether the offer is managed or unmanaged.</span></span>
* <span data-ttu-id="00226-138">지원되는 요금 청구 모델.</span><span class="sxs-lookup"><span data-stu-id="00226-138">Billing models that are supported.</span></span>

<span data-ttu-id="00226-139">SKU는 Marketplace의 부모 제품 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-139">A SKU appears under the parent offer in the Marketplace.</span></span> <span data-ttu-id="00226-140">Azure Portal에는 고유 구입 가능 엔터티로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-140">It appears as its own purchasable entity in the Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="00226-141">제품 설정</span><span class="sxs-lookup"><span data-stu-id="00226-141">Set up an offer</span></span>

1. <span data-ttu-id="00226-142">[클라우드 파트너 포털](https://cloudpartner.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-142">Sign in to the [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="00226-143">왼쪽의 탐색 창에서 **+ 새 제품** > **Azure 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-143">In the navigation pane on the left, select **+ New offer** > **Azure Applications**.</span></span>

    ![새 제품](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="00226-145">**편집기** 보기의 왼쪽에 나타나는 양식을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-145">Fill out the forms that appear on the left in the **Editor** view.</span></span> <span data-ttu-id="00226-146">필수 필드는 빨간색 별표(*)로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-146">Required fields are marked with a red asterisk (*).</span></span>

    ![제품 설정](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="00226-148">관리되는 응용 프로그램을 만드는 데 네 가지 기본 양식이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-148">Four main forms are used to create a managed application:</span></span>

    <span data-ttu-id="00226-149">a.</span><span class="sxs-lookup"><span data-stu-id="00226-149">a.</span></span> <span data-ttu-id="00226-150">제품 설정</span><span class="sxs-lookup"><span data-stu-id="00226-150">Offer Settings</span></span>

    <span data-ttu-id="00226-151">b.</span><span class="sxs-lookup"><span data-stu-id="00226-151">b.</span></span> <span data-ttu-id="00226-152">SKU</span><span class="sxs-lookup"><span data-stu-id="00226-152">SKUs</span></span>

    <span data-ttu-id="00226-153">c.</span><span class="sxs-lookup"><span data-stu-id="00226-153">c.</span></span> <span data-ttu-id="00226-154">마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="00226-154">Marketplace</span></span>

    <span data-ttu-id="00226-155">d.</span><span class="sxs-lookup"><span data-stu-id="00226-155">d.</span></span> <span data-ttu-id="00226-156">지원</span><span class="sxs-lookup"><span data-stu-id="00226-156">Support</span></span>

<span data-ttu-id="00226-157">이러한 양식은 다음 섹션에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-157">These forms are described in greater detail in the following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="00226-158">제품 설정 양식</span><span class="sxs-lookup"><span data-stu-id="00226-158">Offer Settings form</span></span>
<span data-ttu-id="00226-159">이 기본 양식을 사용하여 제품 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-159">Use this basic form to specify the offer settings.</span></span>

1. <span data-ttu-id="00226-160">**제품 설정** 양식을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-160">Fill in the **Offer Settings** form.</span></span> <span data-ttu-id="00226-161">다양한 필드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-161">The different fields are:</span></span>

    <span data-ttu-id="00226-162">a.</span><span class="sxs-lookup"><span data-stu-id="00226-162">a.</span></span> <span data-ttu-id="00226-163">**제품 ID**: 이 고유 식별자는 게시자 프로필 내에서 제품을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-163">**Offer ID**: This unique identifier identifies the offer within a publisher profile.</span></span> <span data-ttu-id="00226-164">이 ID는 제품 URL, Resource Manager 템플릿 및 청구 보고서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="00226-165">소문자 영숫자 문자 또는 대시(-)로만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="00226-166">ID는 대시로 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-166">The ID can't end in a dash.</span></span> <span data-ttu-id="00226-167">최대 50문자로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-167">It's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="00226-168">제품이 라이브 상태가 되면 이 필드는 잠깁니다.</span><span class="sxs-lookup"><span data-stu-id="00226-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="00226-169">b.</span><span class="sxs-lookup"><span data-stu-id="00226-169">b.</span></span> <span data-ttu-id="00226-170">**게시자 ID**: 이 드롭다운 목록을 사용하여 이 제품을 게시하려는 게시자 프로필을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-170">**Publisher ID**: Use this drop-down list to choose the publisher profile you want to publish this offer under.</span></span> <span data-ttu-id="00226-171">제품이 라이브 상태가 되면 이 필드는 잠깁니다.</span><span class="sxs-lookup"><span data-stu-id="00226-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="00226-172">c.</span><span class="sxs-lookup"><span data-stu-id="00226-172">c.</span></span> <span data-ttu-id="00226-173">**이름**: 제품에 대한 이 표시 이름이 Marketplace 및 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-173">**Name**: This display name for your offer appears in the Marketplace and in the portal.</span></span> <span data-ttu-id="00226-174">최대 50문자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="00226-175">제품의 인식 가능한 브랜드 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="00226-176">회사 이름을 포함하는 것이 마케팅 전략인 경우를 제외하고 여기에 회사 이름을 포함하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="00226-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="00226-177">이 제품을 자신의 고유 웹 사이트에 마케팅하는 경우 이 이름은 웹 사이트에 표시되는 이름과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-177">If you're marketing this offer on your own website, ensure that the name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="00226-178">**저장**을 클릭하여 진행 상황을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-178">Select **Save** to save your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="00226-179">SKU 양식</span><span class="sxs-lookup"><span data-stu-id="00226-179">SKUs form</span></span>
<span data-ttu-id="00226-180">다음 단계는 제품에 대한 SKU를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-180">The next step is to add SKUs for your offer.</span></span>

1. <span data-ttu-id="00226-181">**SKU** > **새 SKU**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-181">Select **SKUs** > **New SKU**.</span></span> 

    ![새 SKU 선택](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="00226-183">**SKU ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="00226-184">SKU ID는 제품 내의 SKU에 대한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-184">A SKU ID is a unique identifier for the SKU within an offer.</span></span> <span data-ttu-id="00226-185">이 ID는 제품 URL, Resource Manager 템플릿 및 청구 보고서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="00226-186">소문자 영숫자 문자 또는 대시(-)로만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="00226-187">ID는 대시로 끝내면 안 되며 최대 50문자로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-187">The ID can't end in a dash, and it's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="00226-188">제품이 라이브 상태가 되면 이 필드는 잠깁니다.</span><span class="sxs-lookup"><span data-stu-id="00226-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="00226-189">제품 내에 여러 SKU를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="00226-190">게시하려는 각 이미지에 대해 SKU가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-190">You need a SKU for each image you plan to publish.</span></span>

3. <span data-ttu-id="00226-191">다음 양식의 **SKU 세부 정보** 섹션을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-191">Fill out the **SKU Details** section on the following form:</span></span>

    ![새 SKU 제공](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="00226-193">다음 필드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-193">Fill out the following fields:</span></span>
    
    <span data-ttu-id="00226-194">a.</span><span class="sxs-lookup"><span data-stu-id="00226-194">a.</span></span> <span data-ttu-id="00226-195">**제목**: 이 SKU의 제목을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="00226-196">이 제목은 이 항목에 대한 갤러리에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="00226-196">This title appears in the gallery for this item.</span></span>

    <span data-ttu-id="00226-197">b.</span><span class="sxs-lookup"><span data-stu-id="00226-197">b.</span></span> <span data-ttu-id="00226-198">**요약**: 이 SKU에 대한 간단한 요약을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="00226-199">이 텍스트는 제목 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="00226-199">This text appears underneath the title.</span></span>

    <span data-ttu-id="00226-200">c.</span><span class="sxs-lookup"><span data-stu-id="00226-200">c.</span></span> <span data-ttu-id="00226-201">**설명**: SKU에 대한 자세한 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-201">**Description**: Enter a detailed description about the SKU.</span></span>

    <span data-ttu-id="00226-202">d.</span><span class="sxs-lookup"><span data-stu-id="00226-202">d.</span></span> <span data-ttu-id="00226-203">**SKU 형식**: 허용된 값은 **관리되는 응용 프로그램** 및 **솔루션 템플릿**입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-203">**SKU Type**: The allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="00226-204">이 경우 **관리되는 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="00226-205">다음 양식의 **패키지 세부 정보** 섹션을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-205">Fill out the **Package Details** section on the following form:</span></span>

    ![패키지](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="00226-207">다음 필드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-207">Fill out the following fields:</span></span>

    <span data-ttu-id="00226-208">a.</span><span class="sxs-lookup"><span data-stu-id="00226-208">a.</span></span> <span data-ttu-id="00226-209">**현재 버전**: 업로드하는 패키지에 대한 버전을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-209">**Current Version**: Enter a version for the package you upload.</span></span> <span data-ttu-id="00226-210">`{number}.{number}.{number}{number}` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-210">It should be in the format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="00226-211">b.</span><span class="sxs-lookup"><span data-stu-id="00226-211">b.</span></span> <span data-ttu-id="00226-212">**패키지 파일 선택**: 이 패키지는 .zip 파일로 압축되는 다음 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-212">**Select a package file**: This package contains the following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="00226-213">**applianceMainTemplate.json**: 솔루션/응용 프로그램을 배포하는 데 사용되는 배포 템플릿 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-213">**applianceMainTemplate.json**: The deployment template file that's used to deploy the solution/application.</span></span> <span data-ttu-id="00226-214">배포 템플릿 파일을 작성하는 방법에 대한 정보는 [첫 번째 Azure Resource Manager 템플릿 만들기](resource-manager-create-first-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00226-214">For information about how to create deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="00226-215">**appliancecreateUIDefinition.json**: 이 파일은 Azure Portal에서 이 솔루션/응용 프로그램을 프로비전하는 데 사용되는 사용자 인터페이스를 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-215">**appliancecreateUIDefinition.json**: This file is used by the Azure portal to generate the user interface that's used to provision this solution/application.</span></span> <span data-ttu-id="00226-216">자세한 내용은 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00226-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="00226-217">**mainTemplate.json**: Microsoft.Solution/appliances 리소스만 포함하는 템플릿 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-217">**mainTemplate.json**: This template file contains only the Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="00226-218">mainTemplate 파일에는 다음과 같은 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-218">The mainTemplate file includes the following properties:</span></span>

        *  <span data-ttu-id="00226-219">**kind**: Marketplace에서 관리되는 응용 프로그램으로 **Marketplace**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-219">**kind**: Use **Marketplace** for managed applications in the Marketplace.</span></span>
        *  <span data-ttu-id="00226-220">**ManagedResourceGroupId**: applianceMainTemplate.json에 정의된 모든 리소스가 배포되는 고객 구독에 있는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-220">**ManagedResourceGroupId**: This resource group in the customer's subscription is where all the resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="00226-221">**PublisherPackageId**: 패키지를 고유하게 식별하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-221">**PublisherPackageId**: This string uniquely identifies the package.</span></span> <span data-ttu-id="00226-222">`{publisherId}.{OfferId}.{SKUID}.{PackageVersion}` 형식의 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-222">Provide the value in the format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="00226-223">다음 이미지에 표시된 것처럼 게시 포털에서 **제품 ID** 및 **게시자 ID**를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="00226-223">Obtain the **Offer ID** and **Publisher ID** from the publishing portal, as shown in the following image:</span></span>

![제품 ID](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="00226-225">다음 이미지에 나와 있는 것처럼 **SKU ID**를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="00226-225">Obtain the **SKU ID**, as shown in the following image:</span></span>

![SKU ID](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="00226-227">다음 이미지에 나와 있는 것처럼 패키지 **버전**을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="00226-227">Obtain the package **Version**, as shown in the following image:</span></span>

![패키지 버전](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="00226-229">위의 예제에 따라 **PublisherPackageId**의 값은 `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-229">Based on the preceding examples, the value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="00226-230">샘플 mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="00226-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify the name of the storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

<span data-ttu-id="00226-231">이 패키지는 이 응용 프로그램을 성공적으로 프로비전하는 데 필요한 기타 중첩된 템플릿 또는 스크립트를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-231">This package should contain any other nested templates or scripts that are required to successfully provision this application.</span></span> <span data-ttu-id="00226-232">mainTemplate.json, applianceMainTemplate.json 및 applianceCreateUIDefinition.json 파일은 루트 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-232">The mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at the root folder.</span></span>

* <span data-ttu-id="00226-233">**권한 부여**: 이 속성은 고객 구독에서 리소스에 대해 어떤 사용자가 어떤 수준의 액세스 권한을 갖는지 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-233">**Authorizations**: This property defines who gets access and the level of access to the resources in customers' subscriptions.</span></span> <span data-ttu-id="00226-234">게시자는 이를 사용하여 고객을 대신하여 응용 프로그램을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-234">The publisher can use it to manage the application on behalf of the customer.</span></span>
* <span data-ttu-id="00226-235">**PrincipalId**: 이 속성은 고객 구독에서 리소스에 대한 특정 권한이 부여된 사용자, 사용자 그룹 또는 응용 프로그램의 Azure AD(Azure Active Directory) 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-235">**PrincipalId**: This property is the Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on the resources in the customer's subscription.</span></span> <span data-ttu-id="00226-236">역할 정의는 권한을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-236">The Role Definition describes the permissions.</span></span> 
* <span data-ttu-id="00226-237">**역할 정의**: 이 속성은 Azure AD가 제공한 모든 기본 제공 RBAC(역할 기반 액세스 제어) 역할 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-237">**Role Definition**: This property is a list of all the built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="00226-238">고객을 대신하여 리소스를 관리하는 데 사용할 가장 적합한 역할을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-238">You can select the role that's most appropriate to use to manage the resources on behalf of the customer.</span></span>

<span data-ttu-id="00226-239">여러 권한 부여를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-239">You can add multiple authorizations.</span></span> <span data-ttu-id="00226-240">AD 사용자 그룹을 만들고 **PrincipalId**에서 해당 ID를 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="00226-241">이러한 방식으로 SKU를 업데이트할 필요 없이 사용자 그룹에 더 많은 사용자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-241">This way, you can add more users to the user group without the need to update the SKU.</span></span>

<span data-ttu-id="00226-242">RBAC에 대한 자세한 내용은 [Azure Portal에서 RBAC 시작](../active-directory/role-based-access-control-what-is.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00226-242">For more information about RBAC, see [Get started with RBAC in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="00226-243">Marketplace 양식</span><span class="sxs-lookup"><span data-stu-id="00226-243">Marketplace form</span></span>

<span data-ttu-id="00226-244">Marketplace 양식에서 [Azure Marketplace](https://azuremarketplace.microsoft.com) 및 [Azure Portal](https://portal.azure.com/)에 표시되는 필드를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-244">The Marketplace form asks for fields that show up on the [Azure Marketplace](https://azuremarketplace.microsoft.com) and on the [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="00226-245">미리 보기 구독 ID</span><span class="sxs-lookup"><span data-stu-id="00226-245">Preview subscription IDs</span></span>

<span data-ttu-id="00226-246">게시된 후 제품에 액세스할 수 있는 Azure 구독 ID의 목록을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-246">Enter a list of Azure subscription IDs that can access the offer after it's published.</span></span> <span data-ttu-id="00226-247">이러한 허용 목록 구독을 사용하여 제품을 라이브 상태로 만들기 전에 미리 본 제품을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-247">You can use these white-listed subscriptions to test the previewed offer before you make it live.</span></span> <span data-ttu-id="00226-248">파트너 포털에서 최대 100개의 구독 허용 목록을 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-248">You can compile a white list of up to 100 subscriptions in the partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="00226-249">권장 범주</span><span class="sxs-lookup"><span data-stu-id="00226-249">Suggested categories</span></span>

<span data-ttu-id="00226-250">목록에서 제품이 가장 잘 연결될 수 있는 범주를 5개까지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-250">Select up to five categories from the list that your offer can be best associated with.</span></span> <span data-ttu-id="00226-251">이러한 범주는 고객의 제품을 [Azure Marketplace](https://azuremarketplace.microsoft.com) 및 [Azure Portal](https://portal.azure.com/)에서 사용할 수 있는 제품 범주에 매핑하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-251">These categories are used to map your offer to the product categories that are available in the [Azure Marketplace](https://azuremarketplace.microsoft.com) and the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="00226-252">Azure 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="00226-252">Azure Marketplace</span></span>

<span data-ttu-id="00226-253">관리되는 응용 프로그램 요약은 다음 필드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-253">The summary of your managed application displays the following fields:</span></span>

![Marketplace 요약](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="00226-255">관리되는 응용 프로그램에 대한 **개요** 탭은 다음 필드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-255">The **Overview** tab for your managed application displays the following fields:</span></span>

![마켓플레이스 개요](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="00226-257">관리되는 응용 프로그램에 대한 **계획 + 가격** 탭은 다음 필드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-257">The **Plans + Pricing** tab for your managed application displays the following fields:</span></span>

![Marketplace 계획](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="00226-259">Azure portal</span><span class="sxs-lookup"><span data-stu-id="00226-259">Azure portal</span></span>

<span data-ttu-id="00226-260">관리되는 응용 프로그램 요약은 다음 필드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-260">The summary of your managed application displays the following fields:</span></span>

![포털 요약](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="00226-262">관리되는 응용 프로그램에 대한 개요는 다음 필드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-262">The overview for your managed application displays the following fields:</span></span>

![포털 개요](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="00226-264">로고 지침</span><span class="sxs-lookup"><span data-stu-id="00226-264">Logo guidelines</span></span>

<span data-ttu-id="00226-265">클라우드 파트너 포털에 업로드하는 모든 로고에 대해 이 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="00226-265">Follow these guidelines for any logo that you upload in the Cloud Partner portal:</span></span>

*   <span data-ttu-id="00226-266">Azure 디자인은 단순한 색 팔레트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-266">The Azure design has a simple color palette.</span></span> <span data-ttu-id="00226-267">로고의 기본 색상과 보조 색상 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-267">Limit the number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="00226-268">포털의 테마 색은 흰색과 검은색입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-268">The theme colors of the portal are white and black.</span></span> <span data-ttu-id="00226-269">로고의 배경색으로 이러한 색을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="00226-269">Don't use these colors as the background color for your logo.</span></span> <span data-ttu-id="00226-270">포털에서 로고가 돋보이도록 하는 색을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-270">Use a color that makes your logo prominent in the portal.</span></span> <span data-ttu-id="00226-271">간단한 기본 색을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-271">We recommend simple primary colors.</span></span> <span data-ttu-id="00226-272">*투명한 배경을 사용하는 경우 로고 및 텍스트는 흰색, 검정색 또는 파란색이 아니어야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="00226-272">*If you use a transparent background, make sure that the logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="00226-273">로고의 배경에 그라데이션 효과를 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="00226-273">Don't use a gradient background on the logo.</span></span>
*   <span data-ttu-id="00226-274">로고에 회사 또는 브랜드 이름을 포함한 텍스트를 놓지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="00226-274">Don't place text on the logo, not even your company or brand name.</span></span> <span data-ttu-id="00226-275">로고의 모양과 느낌은 평면적이어야 하며 그라데이션은 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="00226-275">The look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="00226-276">로고가 늘어나지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-276">Make sure the logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="00226-277">대표 로고</span><span class="sxs-lookup"><span data-stu-id="00226-277">Hero logo</span></span>

<span data-ttu-id="00226-278">대표 로고는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="00226-278">The hero logo is optional.</span></span> <span data-ttu-id="00226-279">게시자는 대표 로고를 업로드하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-279">The publisher can choose not to upload a hero logo.</span></span> <span data-ttu-id="00226-280">대표 아이콘을 업로드한 후에 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-280">After the hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="00226-281">이때 파트너는 대표 아이콘에 대한 Marketplace 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-281">At that time, the partner must follow the Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="00226-282">대표 로고 아이콘에 대한 이러한 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="00226-282">Follow these guidelines for the hero logo icon:</span></span>

*   <span data-ttu-id="00226-283">게시자 표시 이름, 계획 제목 및 제품의 자세한 요약은 흰색으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-283">The publisher display name, the plan title, and the offer long summary are displayed in white.</span></span> <span data-ttu-id="00226-284">따라서 대표 아이콘의 배경색으로 밝은 색을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="00226-284">Therefore, don't use a light color for the background of the hero icon.</span></span> <span data-ttu-id="00226-285">대표 아이콘에는 검은색, 흰색 또는 투명한 배경이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="00226-286">제품이 나열되면 대표 로고 안에 게시자 표시 이름, 계획 제목, 자세한 제품 요약과 **만들기** 버튼이 프로그래밍 방식으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-286">After the offer is listed, the publisher display name, the plan title, the offer long summary, and the **Create** button are embedded programmatically inside the hero logo.</span></span> <span data-ttu-id="00226-287">따라서 대표 로고를 디자인하는 동안 텍스트를 입력하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="00226-287">Consequently, don't enter any text while you design the hero logo.</span></span> <span data-ttu-id="00226-288">텍스트는 프로그래밍 방식으로 해당 공간에 포함되므로 오른쪽의 빈 공간을 남겨 둡니다.</span><span class="sxs-lookup"><span data-stu-id="00226-288">Leave empty space on the right because the text is included programmatically in that space.</span></span> <span data-ttu-id="00226-289">오른쪽의 텍스트에 대한 빈 공간은 415x100픽셀이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-289">The empty space for the text should be 415 x 100 pixels on the right.</span></span> <span data-ttu-id="00226-290">왼쪽에서 370픽셀로 오프셋됩니다.</span><span class="sxs-lookup"><span data-stu-id="00226-290">It's offset by 370 pixels from the left.</span></span>

    ![대표 로고 예제](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="00226-292">지원 양식</span><span class="sxs-lookup"><span data-stu-id="00226-292">Support form</span></span>

<span data-ttu-id="00226-293">회사의 지원 연락처로 **지원** 양식을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-293">Fill out the **Support** form with support contacts from your company.</span></span> <span data-ttu-id="00226-294">이 정보는 엔지니어링 연락처와 고객 지원 연락처일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00226-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="00226-295">제품 게시</span><span class="sxs-lookup"><span data-stu-id="00226-295">Publish an offer</span></span>

<span data-ttu-id="00226-296">모든 섹션을 작성한 후 **게시**를 선택하여 고객에게 제품을 제공하는 과정을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00226-296">After you fill out all the sections, select **Publish** to start the process that makes your offer available to customers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00226-297">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00226-297">Next steps</span></span>

* <span data-ttu-id="00226-298">관리되는 응용 프로그램에 대한 소개는 [관리되는 응용 프로그램 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00226-298">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="00226-299">Marketplace의 관리되는 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [Marketplace의 Azure 관리되는 응용 프로그램 사용](managed-application-consume-marketplace.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00226-299">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="00226-300">서비스 카탈로그 관리되는 응용 프로그램을 게시하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 만들기 및 게시](managed-application-publishing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00226-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="00226-301">서비스 카탈로그 관리되는 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 사용](managed-application-consumption.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00226-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>

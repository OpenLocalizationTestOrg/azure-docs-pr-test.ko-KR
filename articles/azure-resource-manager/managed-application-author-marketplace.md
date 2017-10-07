---
title: "aaaAzure 관리 응용 프로그램 마켓플레이스 hello에 | Microsoft Docs"
description: "Azure에 설명 hello 마켓플레이스를 통해 사용할 수 있는 응용 프로그램을 관리 합니다."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="3bb0a-103">Azure는 마켓플레이스 hello에 대 한 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="3bb0a-103">Azure managed applications in hello Marketplace</span></span>

 <span data-ttu-id="3bb0a-104">Msp, Isv 및 시스템 통합자 (SIs) צ ְ ײ Azure 응용 프로그램 toooffer 솔루션 tooall Azure 마켓플레이스 고객을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications toooffer their solutions tooall Azure Marketplace customers.</span></span> <span data-ttu-id="3bb0a-105">이러한 솔루션 hello 유지 관리 및 서비스 고객에 대 한 오버 헤드가 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-105">Such solutions reduce hello maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="3bb0a-106">인프라 및 hello 마켓플레이스를 통해 소프트웨어 게시자 판매할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-106">Publishers can sell infrastructure and software through hello Marketplace.</span></span> <span data-ttu-id="3bb0a-107">서비스 및 운영 지원 toomanaged 응용 프로그램에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-107">They can attach services and operational support toomanaged applications.</span></span> <span data-ttu-id="3bb0a-108">자세한 내용은 [관리되는 응용 프로그램 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="3bb0a-109">MSP, ISV, 또는 SI 수는 응용 프로그램 toohello 마켓플레이스에 게시 방법과 toocustomers 광범위 하 게 사용할 수 있도록이 문서에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-109">This article explains how an MSP, ISV, or SI can publish an application toohello Marketplace and make it broadly available toocustomers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="3bb0a-110">관리되는 응용 프로그램을 게시하기 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="3bb0a-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="3bb0a-111">마켓플레이스 hello에 toolisting 필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="3bb0a-111">Prerequisites toolisting in hello Marketplace:</span></span>

* <span data-ttu-id="3bb0a-112">기술</span><span class="sxs-lookup"><span data-stu-id="3bb0a-112">Technical</span></span>

    *  <span data-ttu-id="3bb0a-113">Hello 기본 구조 및 Azure 리소스 관리자 템플릿 구문에 대 한 정보를 참조 하십시오. [Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-113">For information about hello basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="3bb0a-114">tooview 전체 서식 파일 솔루션 비교 참조 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/en-us/documentation/templates/) 또는 hello [퀵 스타트 템플릿 리포지토리](https://github.com/azure/azure-quickstart-templates)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-114">tooview complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or hello [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="3bb0a-115">Toocreate hello 마켓플레이스를 통해 응용 프로그램을 배포 하는 고객에 대 한 인터페이스를 hello 하는 방법에 대 한 정보를 참조 하십시오. [사용자 인터페이스 정의 파일을 만들](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-115">For information about how toocreate hello interface for customers who deploy your application through hello Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="3bb0a-116">비기술(비즈니스 요구 사항)</span><span class="sxs-lookup"><span data-stu-id="3bb0a-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="3bb0a-117">회사 또는 해당 대리점 판매 hello Marketplace에서 지원 되는 위치는 국가에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-117">Your company or its subsidiary must be located in a country where sales are supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="3bb0a-118">Hello Marketplace에서 지 원하는 청구 모델에 호환 되는 방식으로 제품을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-118">Your product must be licensed in a way that is compatible with billing models supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="3bb0a-119">본인이 기술 지원을 사용할 수 있는 toocustomers 상업적으로 적절 한 방식으로 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-119">You're responsible for making technical support available toocustomers in a commercially reasonable manner.</span></span> <span data-ttu-id="3bb0a-120">hello 지원 될 무료 이며 유료, 하거나 커뮤니티를 통해 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-120">hello support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="3bb0a-121">소프트웨어 및 타사 소프트웨어 종속성에 대해 사용 허가를 받을 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="3bb0a-122">제품 toobe에 대 한 기준에 맞는 콘텐츠 및에 표시 된 hello 마켓플레이스 hello에 Azure 포털을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-122">You must provide content that meets criteria for your offering toobe listed in hello Marketplace and in hello Azure portal.</span></span>
    *   <span data-ttu-id="3bb0a-123">Toohello hello Azure 마켓플레이스 참여 정책 및 게시자 계약 약관을 동의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-123">You must agree toohello terms of hello Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="3bb0a-124">Microsoft Azure 인증 프로그램 계약, hello 사용 약관 및 Microsoft 개인정보취급방침 toocomply를 동의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-124">You must agree toocomply with hello Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="3bb0a-125">새 Azure 응용 프로그램 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb0a-125">Create a new Azure application offer</span></span>

<span data-ttu-id="3bb0a-126">준비 toocreate 후 hello 필수 구성 요소를 충족 하는 관리 되는 응용 프로그램 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-126">After you meet hello prerequisites, you're ready toocreate your managed application offer.</span></span> <span data-ttu-id="3bb0a-127">제품 및 SKU를 간략히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="3bb0a-128">제안</span><span class="sxs-lookup"><span data-stu-id="3bb0a-128">Offer</span></span>

<span data-ttu-id="3bb0a-129">관리 되는 응용 프로그램에 대 한 hello 제공 tooa 클래스는 게시자에서 제공 하는 제품의 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-129">hello offer for a managed application corresponds tooa class of product offering from a publisher.</span></span> <span data-ttu-id="3bb0a-130">새로운 유형의 솔루션/응용 프로그램 원하는 toomake hello 시장에서에서 사용할 수 있는 경우 새 제안을으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-130">If you have a new type of solution/application that you want toomake available in hello Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="3bb0a-131">제품은 SKU의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="3bb0a-132">모든 제안 hello Marketplace의에서 고유 엔터티로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-132">Every offer appears as its own entity in hello Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="3bb0a-133">SKU</span><span class="sxs-lookup"><span data-stu-id="3bb0a-133">SKU</span></span>

<span data-ttu-id="3bb0a-134">SKU는 hello 가장 작은 있는 구입 가능한 단위 제안의입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-134">A SKU is hello smallest purchasable unit of an offer.</span></span> <span data-ttu-id="3bb0a-135">Hello 내 SKU를 사용할 수 있습니다 간에 동일한 제품 클래스 (제안) toodifferentiate:</span><span class="sxs-lookup"><span data-stu-id="3bb0a-135">You can use a SKU within hello same product class (offer) toodifferentiate between:</span></span>

* <span data-ttu-id="3bb0a-136">제공되는 다양한 기능.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-136">Different features that are supported.</span></span>
* <span data-ttu-id="3bb0a-137">Hello 제공 관리 또는 관리 되지 않는 여부</span><span class="sxs-lookup"><span data-stu-id="3bb0a-137">Whether hello offer is managed or unmanaged.</span></span>
* <span data-ttu-id="3bb0a-138">지원되는 요금 청구 모델.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-138">Billing models that are supported.</span></span>

<span data-ttu-id="3bb0a-139">SKU는 hello Marketplace에서에서 hello 부모 제공 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-139">A SKU appears under hello parent offer in hello Marketplace.</span></span> <span data-ttu-id="3bb0a-140">Hello Azure 포털에에서 있는 구입 가능한 자체 엔터티로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-140">It appears as its own purchasable entity in hello Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="3bb0a-141">제품 설정</span><span class="sxs-lookup"><span data-stu-id="3bb0a-141">Set up an offer</span></span>

1. <span data-ttu-id="3bb0a-142">Toohello 로그인 [클라우드 파트너 포털](https://cloudpartner.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-142">Sign in toohello [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="3bb0a-143">Hello hello 왼쪽의 탐색 창에서 선택 **+ 새 제안을** > **Azure 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-143">In hello navigation pane on hello left, select **+ New offer** > **Azure Applications**.</span></span>

    ![새 제품](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="3bb0a-145">Hello에 남아 있는 hello에 나타나는 hello 양식을 작성 **편집기** 보기.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-145">Fill out hello forms that appear on hello left in hello **Editor** view.</span></span> <span data-ttu-id="3bb0a-146">필수 필드는 빨간색 별표(*)로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-146">Required fields are marked with a red asterisk (*).</span></span>

    ![제품 설정](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="3bb0a-148">4 개의 주 폼은 관리 되는 응용 프로그램을 사용 하는 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-148">Four main forms are used toocreate a managed application:</span></span>

    <span data-ttu-id="3bb0a-149">a.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-149">a.</span></span> <span data-ttu-id="3bb0a-150">제품 설정</span><span class="sxs-lookup"><span data-stu-id="3bb0a-150">Offer Settings</span></span>

    <span data-ttu-id="3bb0a-151">b.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-151">b.</span></span> <span data-ttu-id="3bb0a-152">SKU</span><span class="sxs-lookup"><span data-stu-id="3bb0a-152">SKUs</span></span>

    <span data-ttu-id="3bb0a-153">c.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-153">c.</span></span> <span data-ttu-id="3bb0a-154">마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="3bb0a-154">Marketplace</span></span>

    <span data-ttu-id="3bb0a-155">d.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-155">d.</span></span> <span data-ttu-id="3bb0a-156">지원</span><span class="sxs-lookup"><span data-stu-id="3bb0a-156">Support</span></span>

<span data-ttu-id="3bb0a-157">이러한 폼 hello 다음 섹션에서에서 자세히 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-157">These forms are described in greater detail in hello following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="3bb0a-158">제품 설정 양식</span><span class="sxs-lookup"><span data-stu-id="3bb0a-158">Offer Settings form</span></span>
<span data-ttu-id="3bb0a-159">이 기본 형식은 toospecify hello 제안 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-159">Use this basic form toospecify hello offer settings.</span></span>

1. <span data-ttu-id="3bb0a-160">Hello 입력 **설정을 제공** 폼입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-160">Fill in hello **Offer Settings** form.</span></span> <span data-ttu-id="3bb0a-161">hello 다른 필드는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-161">hello different fields are:</span></span>

    <span data-ttu-id="3bb0a-162">a.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-162">a.</span></span> <span data-ttu-id="3bb0a-163">**제안 ID**:이 고유 식별자 게시자 프로필 내에서 hello 제품을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-163">**Offer ID**: This unique identifier identifies hello offer within a publisher profile.</span></span> <span data-ttu-id="3bb0a-164">이 ID는 제품 URL, Resource Manager 템플릿 및 청구 보고서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="3bb0a-165">소문자 영숫자 문자 또는 대시(-)로만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="3bb0a-166">hello ID에 대시 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-166">hello ID can't end in a dash.</span></span> <span data-ttu-id="3bb0a-167">최대 50 자로 제한 tooa 것합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-167">It's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="3bb0a-168">제품이 라이브 상태가 되면 이 필드는 잠깁니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="3bb0a-169">b.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-169">b.</span></span> <span data-ttu-id="3bb0a-170">**게시자 ID**: toopublish 아래에서이 서비스를 원하는이 드롭다운 목록에서 toochoose hello 게시자 프로필을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-170">**Publisher ID**: Use this drop-down list toochoose hello publisher profile you want toopublish this offer under.</span></span> <span data-ttu-id="3bb0a-171">제품이 라이브 상태가 되면 이 필드는 잠깁니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="3bb0a-172">c.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-172">c.</span></span> <span data-ttu-id="3bb0a-173">**이름**: hello 포털 및 hello Marketplace에에서 자신의 구독에 대 한이 표시 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-173">**Name**: This display name for your offer appears in hello Marketplace and in hello portal.</span></span> <span data-ttu-id="3bb0a-174">최대 50문자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="3bb0a-175">제품의 인식 가능한 브랜드 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="3bb0a-176">회사 이름을 포함하는 것이 마케팅 전략인 경우를 제외하고 여기에 회사 이름을 포함하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="3bb0a-177">자신의 웹 사이트에이 서비스를 마케팅 하는 경우 hello 이름이 확인 정확 하 게 웹 사이트에 표시 되는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-177">If you're marketing this offer on your own website, ensure that hello name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="3bb0a-178">선택 **저장** toosave 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-178">Select **Save** toosave your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="3bb0a-179">SKU 양식</span><span class="sxs-lookup"><span data-stu-id="3bb0a-179">SKUs form</span></span>
<span data-ttu-id="3bb0a-180">hello 다음 단계에 대 한 제안 tooadd Sku입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-180">hello next step is tooadd SKUs for your offer.</span></span>

1. <span data-ttu-id="3bb0a-181">**SKU** > **새 SKU**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-181">Select **SKUs** > **New SKU**.</span></span> 

    ![새 SKU 선택](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="3bb0a-183">**SKU ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="3bb0a-184">SKU ID는 제공 하는 서비스 내에서 SKU hello에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-184">A SKU ID is a unique identifier for hello SKU within an offer.</span></span> <span data-ttu-id="3bb0a-185">이 ID는 제품 URL, Resource Manager 템플릿 및 청구 보고서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="3bb0a-186">소문자 영숫자 문자 또는 대시(-)로만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="3bb0a-187">hello ID에 대시를 끝나서는 안 되며 최대 50 자로 제한 tooa 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-187">hello ID can't end in a dash, and it's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="3bb0a-188">제품이 라이브 상태가 되면 이 필드는 잠깁니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="3bb0a-189">제품 내에 여러 SKU를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="3bb0a-190">필요한 SKU toopublish 각 이미지에 대 한 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-190">You need a SKU for each image you plan toopublish.</span></span>

3. <span data-ttu-id="3bb0a-191">Hello 채울 **SKU 세부 정보** hello 다음 양식에서 섹션:</span><span class="sxs-lookup"><span data-stu-id="3bb0a-191">Fill out hello **SKU Details** section on hello following form:</span></span>

    ![새 SKU 제공](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="3bb0a-193">Hello 다음 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-193">Fill out hello following fields:</span></span>
    
    <span data-ttu-id="3bb0a-194">a.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-194">a.</span></span> <span data-ttu-id="3bb0a-195">**제목**: 이 SKU의 제목을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="3bb0a-196">이 항목에 대 한 hello 갤러리에서이 제목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-196">This title appears in hello gallery for this item.</span></span>

    <span data-ttu-id="3bb0a-197">b.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-197">b.</span></span> <span data-ttu-id="3bb0a-198">**요약**: 이 SKU에 대한 간단한 요약을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="3bb0a-199">이 텍스트 hello 제목 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-199">This text appears underneath hello title.</span></span>

    <span data-ttu-id="3bb0a-200">c.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-200">c.</span></span> <span data-ttu-id="3bb0a-201">**설명**: hello SKU에 대 한 자세한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-201">**Description**: Enter a detailed description about hello SKU.</span></span>

    <span data-ttu-id="3bb0a-202">d.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-202">d.</span></span> <span data-ttu-id="3bb0a-203">**SKU 유형의**: hello 가능한 값은 **관리 응용 프로그램** 및 **솔루션 템플릿을**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-203">**SKU Type**: hello allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="3bb0a-204">이 경우 **관리되는 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="3bb0a-205">Hello 채울 **패키지 세부 정보** hello 다음 양식에서 섹션:</span><span class="sxs-lookup"><span data-stu-id="3bb0a-205">Fill out hello **Package Details** section on hello following form:</span></span>

    ![패키지](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="3bb0a-207">Hello 다음 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-207">Fill out hello following fields:</span></span>

    <span data-ttu-id="3bb0a-208">a.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-208">a.</span></span> <span data-ttu-id="3bb0a-209">**현재 버전**: hello 패키지 업로드에 대 한 버전을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-209">**Current Version**: Enter a version for hello package you upload.</span></span> <span data-ttu-id="3bb0a-210">Hello 형태로 표시 것 `{number}.{number}.{number}{number}`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-210">It should be in hello format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="3bb0a-211">b.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-211">b.</span></span> <span data-ttu-id="3bb0a-212">**패키지 파일을 선택**: hello.zip 파일로 압축 된 파일을 다음이 패키지에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-212">**Select a package file**: This package contains hello following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="3bb0a-213">**applianceMainTemplate.json**: toodeploy hello 솔루션/응용 프로그램을 사용 하는 hello 배포 템플릿 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-213">**applianceMainTemplate.json**: hello deployment template file that's used toodeploy hello solution/application.</span></span> <span data-ttu-id="3bb0a-214">방법에 대 한 내용은 toocreate 배포 템플릿 파일을 참조 하세요. [첫 번째 Azure 리소스 관리자 서식 파일 만들기](resource-manager-create-first-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-214">For information about how toocreate deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="3bb0a-215">**appliancecreateUIDefinition.json**:이 파일은 tooprovision이 솔루션/응용 프로그램 사용 hello Azure 포털 toogenerate hello 사용자 인터페이스에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-215">**appliancecreateUIDefinition.json**: This file is used by hello Azure portal toogenerate hello user interface that's used tooprovision this solution/application.</span></span> <span data-ttu-id="3bb0a-216">자세한 내용은 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="3bb0a-217">**mainTemplate.json**:이 템플릿 파일 hello Microsoft.Solution/appliances 리소스만 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-217">**mainTemplate.json**: This template file contains only hello Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="3bb0a-218">hello mainTemplate 파일 hello를 다음 속성이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-218">hello mainTemplate file includes hello following properties:</span></span>

        *  <span data-ttu-id="3bb0a-219">**종류**: 사용 **마켓플레이스** hello Marketplace에서에서 관리 되는 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-219">**kind**: Use **Marketplace** for managed applications in hello Marketplace.</span></span>
        *  <span data-ttu-id="3bb0a-220">**ManagedResourceGroupId**: hello 고객의 구독에서이 리소스 그룹은 applianceMainTemplate.json에 정의 된 모든 hello 리소스 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-220">**ManagedResourceGroupId**: This resource group in hello customer's subscription is where all hello resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="3bb0a-221">**PublisherPackageId**:이 문자열 hello 패키지를 고유 하 게 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-221">**PublisherPackageId**: This string uniquely identifies hello package.</span></span> <span data-ttu-id="3bb0a-222">Hello 형태로 표시의 hello 값을 제공 `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-222">Provide hello value in hello format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="3bb0a-223">Hello 가져올 **ID 제공** 및 **게시자 ID** hello 다음 이미지와 같이 포털을 게시 하는 hello에서:</span><span class="sxs-lookup"><span data-stu-id="3bb0a-223">Obtain hello **Offer ID** and **Publisher ID** from hello publishing portal, as shown in hello following image:</span></span>

![제품 ID](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="3bb0a-225">Hello 가져올 **SKU ID**hello 다음 이미지에에서 나타난 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="3bb0a-225">Obtain hello **SKU ID**, as shown in hello following image:</span></span>

![SKU ID](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="3bb0a-227">Hello 패키지를 다운로드 **버전**hello 다음 이미지에에서 나타난 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="3bb0a-227">Obtain hello package **Version**, as shown in hello following image:</span></span>

![패키지 버전](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="3bb0a-229">값을 hello 앞 예제는 hello에 따라, **PublisherPackageId** 은 `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-229">Based on hello preceding examples, hello value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="3bb0a-230">샘플 mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="3bb0a-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
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

<span data-ttu-id="3bb0a-231">이 패키지는 다른 중첩 된 템플릿에 있어야 하거나 필요한 toosuccessfully 되는 스크립트를이 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-231">This package should contain any other nested templates or scripts that are required toosuccessfully provision this application.</span></span> <span data-ttu-id="3bb0a-232">hello mainTemplate.json, applianceMainTemplate.json, 및 applianceCreateUIDefinition.json 파일이 있어야 hello 루트 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-232">hello mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at hello root folder.</span></span>

* <span data-ttu-id="3bb0a-233">**권한 부여**:이 속성은 액세스 및 hello 수준의 액세스를 가져옵니다는 고객의 구독에서 toohello 리소스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-233">**Authorizations**: This property defines who gets access and hello level of access toohello resources in customers' subscriptions.</span></span> <span data-ttu-id="3bb0a-234">hello 게시자 toomanage hello 응용 프로그램 hello 고객을 대신 하 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-234">hello publisher can use it toomanage hello application on behalf of hello customer.</span></span>
* <span data-ttu-id="3bb0a-235">**PrincipalId**:이 속성은 사용자, 사용자 그룹 또는 응용 프로그램 hello 고객의 구독에서 hello 리소스에 대 한 특정 권한 부여의 hello Azure Active Directory (Azure AD) 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-235">**PrincipalId**: This property is hello Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on hello resources in hello customer's subscription.</span></span> <span data-ttu-id="3bb0a-236">역할 정의 hello hello 권한을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-236">hello Role Definition describes hello permissions.</span></span> 
* <span data-ttu-id="3bb0a-237">**역할 정의**:이 속성은 역할의 목록을 모든 hello 기본 제공 역할 기반 액세스 제어 (RBAC) Azure AD에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-237">**Role Definition**: This property is a list of all hello built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="3bb0a-238">Hello 고객을 대신 하 여 가장 적합 한 toouse toomanage hello 리소스는 hello 역할을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-238">You can select hello role that's most appropriate toouse toomanage hello resources on behalf of hello customer.</span></span>

<span data-ttu-id="3bb0a-239">여러 권한 부여를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-239">You can add multiple authorizations.</span></span> <span data-ttu-id="3bb0a-240">AD 사용자 그룹을 만들고 **PrincipalId**에서 해당 ID를 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="3bb0a-241">이러한 방식으로 hello 필요 tooupdate hello SKU 없이 더 많은 사용자가 toohello 사용자 그룹을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-241">This way, you can add more users toohello user group without hello need tooupdate hello SKU.</span></span>

<span data-ttu-id="3bb0a-242">RBAC에 대 한 자세한 내용은 참조 [hello Azure 포털에에서 RBAC 시작](../active-directory/role-based-access-control-what-is.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-242">For more information about RBAC, see [Get started with RBAC in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="3bb0a-243">Marketplace 양식</span><span class="sxs-lookup"><span data-stu-id="3bb0a-243">Marketplace form</span></span>

<span data-ttu-id="3bb0a-244">마켓플레이스 폼 hello hello에 표시 되는 필드에 대 한 요청 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com) hello에 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-244">hello Marketplace form asks for fields that show up on hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and on hello [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="3bb0a-245">미리 보기 구독 ID</span><span class="sxs-lookup"><span data-stu-id="3bb0a-245">Preview subscription IDs</span></span>

<span data-ttu-id="3bb0a-246">Azure 구독 Id가 게시 된 후 hello 제안에 액세스할 수 있는 목록을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-246">Enter a list of Azure subscription IDs that can access hello offer after it's published.</span></span> <span data-ttu-id="3bb0a-247">수행 하기 전에 이러한 구독 허용 목록을 tootest hello 미리 본 제품을 사용할 수 있습니다 라이브 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-247">You can use these white-listed subscriptions tootest hello previewed offer before you make it live.</span></span> <span data-ttu-id="3bb0a-248">Hello 파트너 포털에서 too100 구독을의 허용 목록을 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-248">You can compile a white list of up too100 subscriptions in hello partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="3bb0a-249">권장 범주</span><span class="sxs-lookup"><span data-stu-id="3bb0a-249">Suggested categories</span></span>

<span data-ttu-id="3bb0a-250">제안을 가장 된 연결 될 수 있는 hello 목록에서 toofive 범주를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-250">Select up toofive categories from hello list that your offer can be best associated with.</span></span> <span data-ttu-id="3bb0a-251">이러한 범주는 사용 되는 toomap hello에서 사용할 수 있는 사용자 제공 toohello 제품 범주 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com) 및 hello [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-251">These categories are used toomap your offer toohello product categories that are available in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="3bb0a-252">Azure 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="3bb0a-252">Azure Marketplace</span></span>

<span data-ttu-id="3bb0a-253">관리 되는 응용 프로그램의 hello 요약 hello를 다음 필드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-253">hello summary of your managed application displays hello following fields:</span></span>

![Marketplace 요약](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="3bb0a-255">hello **개요** 탭에 관리 되는 응용 프로그램에 필드 다음 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-255">hello **Overview** tab for your managed application displays hello following fields:</span></span>

![마켓플레이스 개요](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="3bb0a-257">hello **계획 + 가격 책정** 탭에 관리 되는 응용 프로그램에 필드 다음 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-257">hello **Plans + Pricing** tab for your managed application displays hello following fields:</span></span>

![Marketplace 계획](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="3bb0a-259">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3bb0a-259">Azure portal</span></span>

<span data-ttu-id="3bb0a-260">관리 되는 응용 프로그램의 hello 요약 hello를 다음 필드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-260">hello summary of your managed application displays hello following fields:</span></span>

![포털 요약](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="3bb0a-262">관리 되는 응용 프로그램에 대 한 hello 개요 hello를 다음 필드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-262">hello overview for your managed application displays hello following fields:</span></span>

![포털 개요](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="3bb0a-264">로고 지침</span><span class="sxs-lookup"><span data-stu-id="3bb0a-264">Logo guidelines</span></span>

<span data-ttu-id="3bb0a-265">Hello 클라우드 파트너 포털에 업로드 하는 모든 로고에 대 한 이러한 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-265">Follow these guidelines for any logo that you upload in hello Cloud Partner portal:</span></span>

*   <span data-ttu-id="3bb0a-266">hello Azure 디자인 간단한 색상표를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-266">hello Azure design has a simple color palette.</span></span> <span data-ttu-id="3bb0a-267">Hello 수가 기본과 보조 색 로고에 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-267">Limit hello number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="3bb0a-268">hello 포털의 hello 테마 색 흰색은 검정입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-268">hello theme colors of hello portal are white and black.</span></span> <span data-ttu-id="3bb0a-269">로고에 대 한 hello 배경색으로 이러한 색을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-269">Don't use these colors as hello background color for your logo.</span></span> <span data-ttu-id="3bb0a-270">Hello 포털에서 관련성이 로고 하는 색을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-270">Use a color that makes your logo prominent in hello portal.</span></span> <span data-ttu-id="3bb0a-271">간단한 기본 색을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-271">We recommend simple primary colors.</span></span> <span data-ttu-id="3bb0a-272">*투명 한 배경을 사용 하는 경우 hello 로고와 텍스트 흰색이 아닌 있는지 확인 검정, 또는 파란색입니다.*</span><span class="sxs-lookup"><span data-stu-id="3bb0a-272">*If you use a transparent background, make sure that hello logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="3bb0a-273">그라데이션 배경이 hello 로고에 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-273">Don't use a gradient background on hello logo.</span></span>
*   <span data-ttu-id="3bb0a-274">Hello 로고, 하더라도 회사 또는 브랜드 이름에 텍스트를 배치 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-274">Don't place text on hello logo, not even your company or brand name.</span></span> <span data-ttu-id="3bb0a-275">로고의 hello 모양과 느낌 플랫와 기울기를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-275">hello look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="3bb0a-276">Hello 로고 확대 되지 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-276">Make sure hello logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="3bb0a-277">대표 로고</span><span class="sxs-lookup"><span data-stu-id="3bb0a-277">Hero logo</span></span>

<span data-ttu-id="3bb0a-278">hello hero 로고 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-278">hello hero logo is optional.</span></span> <span data-ttu-id="3bb0a-279">hello 게시자 하지 tooupload hero 로고를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-279">hello publisher can choose not tooupload a hero logo.</span></span> <span data-ttu-id="3bb0a-280">Hello hero 아이콘을 업로드 한 후에 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-280">After hello hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="3bb0a-281">그 당시 hello 파트너 hero 아이콘에 대 한 hello 마켓플레이스 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-281">At that time, hello partner must follow hello Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="3bb0a-282">Hello hero 로고 아이콘에 대 한 이러한 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-282">Follow these guidelines for hello hero logo icon:</span></span>

*   <span data-ttu-id="3bb0a-283">hello 게시자 표시 이름, hello 계획 제목 및 긴 요약 hello 제공 흰색으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-283">hello publisher display name, hello plan title, and hello offer long summary are displayed in white.</span></span> <span data-ttu-id="3bb0a-284">따라서 사용 하지 마십시오 밝은 색 hello hero 아이콘의 hello 배경색입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-284">Therefore, don't use a light color for hello background of hello hero icon.</span></span> <span data-ttu-id="3bb0a-285">대표 아이콘에는 검은색, 흰색 또는 투명한 배경이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="3bb0a-286">Hello 제안을 나열 됩니다 hello 게시자 표시 이름, hello 계획 제목, 긴 요약 hello 제안 및 hello **만들기** 단추 hello hero 로고에 프로그래밍 방식으로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-286">After hello offer is listed, hello publisher display name, hello plan title, hello offer long summary, and hello **Create** button are embedded programmatically inside hello hero logo.</span></span> <span data-ttu-id="3bb0a-287">따라서 하지 hello hero 로고를 디자인 하는 동안 텍스트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-287">Consequently, don't enter any text while you design hello hero logo.</span></span> <span data-ttu-id="3bb0a-288">빈 공간 hello에 오른쪽 것 이므로 유지 hello 텍스트가 해당 공간에에서 프로그래밍 방식으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-288">Leave empty space on hello right because hello text is included programmatically in that space.</span></span> <span data-ttu-id="3bb0a-289">hello 텍스트에 대 한 hello 빈 공간 hello 오른쪽에 415 x 100 픽셀 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-289">hello empty space for hello text should be 415 x 100 pixels on hello right.</span></span> <span data-ttu-id="3bb0a-290">Hello 왼쪽에서 370 픽셀로 오프셋 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-290">It's offset by 370 pixels from hello left.</span></span>

    ![대표 로고 예제](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="3bb0a-292">지원 양식</span><span class="sxs-lookup"><span data-stu-id="3bb0a-292">Support form</span></span>

<span data-ttu-id="3bb0a-293">Hello 채울 **지원** 회사에서 지 원하는 폼에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-293">Fill out hello **Support** form with support contacts from your company.</span></span> <span data-ttu-id="3bb0a-294">이 정보는 엔지니어링 연락처와 고객 지원 연락처일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="3bb0a-295">제품 게시</span><span class="sxs-lookup"><span data-stu-id="3bb0a-295">Publish an offer</span></span>

<span data-ttu-id="3bb0a-296">모든 hello 섹션을 입력 한 후 선택 **게시** 제안을 사용할 수 있는 toocustomers 하는 toostart hello 프로세스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-296">After you fill out all hello sections, select **Publish** toostart hello process that makes your offer available toocustomers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bb0a-297">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3bb0a-297">Next steps</span></span>

* <span data-ttu-id="3bb0a-298">소개 toomanaged 응용 프로그램에 대 한 참조 [관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-298">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="3bb0a-299">Hello 시장에서에서 관리 되는 응용 프로그램을 사용 하는 방법에 대 한 정보를 참조 하십시오. [사용할 Azure 관리 응용 프로그램 마켓플레이스 hello에](managed-application-consume-marketplace.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-299">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="3bb0a-300">서비스 카탈로그 관리되는 응용 프로그램을 게시하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 만들기 및 게시](managed-application-publishing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="3bb0a-301">서비스 카탈로그 관리되는 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 사용](managed-application-consumption.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3bb0a-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>

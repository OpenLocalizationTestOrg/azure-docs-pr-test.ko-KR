---
title: "hello Azure Marketplace의에서 가상 컴퓨터 이미지 aaaManaging | Microsoft Docs"
description: "어떻게 toomanage 가상 컴퓨터 이미지 hello Azure Marketplace에서에서 초기 게시 한 후에 자세한 가이드"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a><span data-ttu-id="c070d-103">가상 컴퓨터에 대 한 제작 후 가이드 hello Azure Marketplace에서 제공</span><span class="sxs-lookup"><span data-stu-id="c070d-103">Post-production guide for virtual machine offers in hello Azure Marketplace</span></span>
<span data-ttu-id="c070d-104">이 문서는 가상 컴퓨터 실시간 행사 hello Azure Marketplace에서에서 업데이트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-104">This article explains how you can update a live virtual machine offer in hello Azure Marketplace.</span></span> <span data-ttu-id="c070d-105">하나 이상의 새 Sku tooan 기존 제안을 추가 hello 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-105">It guides you through hello process of adding one or more new SKUs tooan existing offer.</span></span> <span data-ttu-id="c070d-106">또한 과정을 안내 hello 프로세스 hello Marketplace에서에서 가상 컴퓨터 실시간 제안 또는 SKU를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-106">It also guides you through hello process of removing a live virtual machine offer or SKU from hello Marketplace.</span></span>

<span data-ttu-id="c070d-107">Hello에 제안을/SKU를 준비 하는 후 [Azure 포털](http://portal.azure.com), hello 텍스트 상자에 다음을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-107">After an offer/SKU is staged in hello [Azure portal](http://portal.azure.com), you can't change hello following text boxes:</span></span>

* <span data-ttu-id="c070d-108">**식별자를 제공**: hello 게시 포털 이동 너무**가상 컴퓨터** 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-108">**Offer Identifier**: In hello Publishing portal, go too**virtual machines** and select your offer.</span></span> <span data-ttu-id="c070d-109">**VM 이미지** > **제품 식별자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-109">Then click **VM IMAGES** > **Offer Identifier**.</span></span>
* <span data-ttu-id="c070d-110">**SKU 식별자**: hello 게시 포털 이동 너무**가상 컴퓨터** 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-110">**SKU Identifier**: In hello Publishing portal, go too**virtual machines** and select your offer.</span></span> <span data-ttu-id="c070d-111">**SKU** > **SKU 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-111">Then click **SKUS** > **Add a SKU**.</span></span>
* <span data-ttu-id="c070d-112">**게시자 Namespace**: hello 게시 포털 이동 너무**가상 컴퓨터** > **연습** > **알려 주세요.에 대 한 사용자 회사** ("단계 2 등록 Your Company" 아래에서 찾을 수) > **게시자 Namespace** > **Namespace**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-112">**Publisher Namespace**: In hello Publishing portal, go too**virtual machines** > **Walkthrough** > **Tell Us About Your Company** (found under “Step 2 Register Your Company”) > **Publisher Namespace** > **Namespace**.</span></span>

<span data-ttu-id="c070d-113">Hello 제공/SKU hello에 나열 된 후 [마켓플레이스](http://azure.microsoft.com/marketplace), hello 텍스트 상자에 다음을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-113">After hello offer/SKU is listed in hello [Marketplace](http://azure.microsoft.com/marketplace), you can't change hello following text boxes:</span></span>

* <span data-ttu-id="c070d-114">**식별자를 제공**: hello 게시 포털 이동 너무**가상 컴퓨터** 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-114">**Offer Identifier**: In hello Publishing portal, go too**virtual machines** and select your offer.</span></span> <span data-ttu-id="c070d-115">**VM 이미지** > **제품 식별자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-115">Then click **VM IMAGES** > **Offer Identifier**.</span></span>
* <span data-ttu-id="c070d-116">**SKU 식별자**: hello 게시 포털 이동 너무**가상 컴퓨터** 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-116">**SKU Identifier**: In hello Publishing portal, go too**virtual machines** and select your offer.</span></span> <span data-ttu-id="c070d-117">**SKU** > **SKU 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-117">Then click **SKUS** > **Add a SKU**.</span></span>
* <span data-ttu-id="c070d-118">**게시자 Namespace**: hello 게시 포털 이동 너무**가상 컴퓨터** > **연습** > **알려 주세요.에 대 한 사용자 회사** ("단계 2 등록" 아래에서 찾을 수) **게시자 Namespace** > **Namespace**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-118">**Publisher Namespace**: In hello Publishing portal, go too**virtual machines** > **Walkthrough** > **Tell Us About Your Company** (found under "Step 2 Register") **Publisher Namespace** > **Namespace**.</span></span>
* <span data-ttu-id="c070d-119">**포트**: hello 게시 포털 이동 너무**가상 컴퓨터** 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-119">**Ports**: In hello Publishing portal, go too**virtual machines** and select your offer.</span></span> <span data-ttu-id="c070d-120">**VM 이미지** > **포트 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-120">Then click **VM IMAGES** > **Open Ports**.</span></span>
* <span data-ttu-id="c070d-121">**나열된 SKU의 가격 책정 변경**</span><span class="sxs-lookup"><span data-stu-id="c070d-121">**Pricing change of listed SKU(s)**</span></span>
* <span data-ttu-id="c070d-122">**나열된 SKU의 청구 모델 변경**</span><span class="sxs-lookup"><span data-stu-id="c070d-122">**Billing model change of listed SKU(s)**</span></span>
* <span data-ttu-id="c070d-123">**나열된 SKU의 청구 지역 제거**</span><span class="sxs-lookup"><span data-stu-id="c070d-123">**Removal of billing regions of listed SKU(s)**</span></span>
* <span data-ttu-id="c070d-124">**변화 하는 hello 데이터 디스크 나열된 SKU(s) 개수**</span><span class="sxs-lookup"><span data-stu-id="c070d-124">**Changing hello data disk count of listed SKU(s)**</span></span>

## <a name="update-hello-technical-details-of-a-sku"></a><span data-ttu-id="c070d-125">SKU의 hello 기술 세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="c070d-125">Update hello technical details of a SKU</span></span>
<span data-ttu-id="c070d-126">새 버전 toohello tooadd SKU를 나열 하 고 자신의 구독을 다시 게시, 다음이 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="c070d-126">tooadd a new version toohello listed SKU and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="c070d-127">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-127">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="c070d-128">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-128">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-129">Hello hello 왼쪽 메뉴를 클릭 hello **VM 이미지** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-129">In hello menu on hello left, click hello **VM IMAGES** tab.</span></span>
4. <span data-ttu-id="c070d-130">Hello에 **Sku** 섹션에서 hello tooupdate SKU를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-130">In hello **SKUs** section, locate hello SKU that you want tooupdate.</span></span>
5. <span data-ttu-id="c070d-131">Hello SKU에 대 한 새 버전 번호를 추가 하 고 hello 클릭  **+**  단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-131">Add a new version number for hello SKU, and click hello **+** button.</span></span> <span data-ttu-id="c070d-132">hello 새 버전은 X, Y 및 Z는 정수 x.y.z 형식이 며 형식에서 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-132">hello new version should be in an X.Y.Z format, where X, Y, and Z are integers.</span></span> <span data-ttu-id="c070d-133">버전 변경은 증분되어야만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-133">Version changes should only be incremental.</span></span>
6. <span data-ttu-id="c070d-134">Hello에 **OS VHD URL** 상자 hello 공유 액세스 서명 URI 생성 hello 운영 체제 VHD에 대 한 입력 하 고 hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-134">In hello **OS VHD URL** box, enter hello shared access signature URI created for hello operating system VHD and save hello changes.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c070d-135">있습니다 수 증가/감소 나열 된 SKU의 hello 데이터 디스크 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-135">You can't increment/decrement hello data disk count of a listed SKU.</span></span> <span data-ttu-id="c070d-136">이 경우 새로운 SKU toocreate가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-136">You need toocreate a new SKU in this case.</span></span> <span data-ttu-id="c070d-137">자세한 지침은 toohello 섹션을 참조 하십시오. [아래 나열 된 제품은 새로운 SKU 추가](#add-a-new-sku-under-a-listed-offer)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-137">For detailed guidance, refer toohello section [Add a new SKU under a listed offer](#add-a-new-sku-under-a-listed-offer).</span></span>
   >
   >
7. <span data-ttu-id="c070d-138">Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-138">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="c070d-139">참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-139">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="c070d-140">제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-140">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-141">클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-141">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![VM 이미지](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a><span data-ttu-id="c070d-143">제공 하는 서비스 또는 SKU의 hello 기술 세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="c070d-143">Update hello nontechnical details of an offer or a SKU</span></span>
<span data-ttu-id="c070d-144">Hello 배경이 (마케팅, 법률, 지원, 범주)을 업데이트할 수 있습니다 hello Marketplace에서에서 라이브 제안 또는 SKU의 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-144">You can update hello nontechnical (marketing, legal, support, categories) details of your live offer or SKU in hello Marketplace.</span></span>

### <a name="update-hello-offer-description-and-logos"></a><span data-ttu-id="c070d-145">Hello 서비스 설명 및 로고를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-145">Update hello offer description and logos</span></span>
<span data-ttu-id="c070d-146">tooupdate hello 세부 정보를 제공 하 고 자신의 구독을 다시 게시, 다음이 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="c070d-146">tooupdate hello offer details and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="c070d-147">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-147">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="c070d-148">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-148">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-149">Hello hello 왼쪽 메뉴를 클릭 hello **마케팅** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-149">In hello menu on hello left, click hello **MARKETING** tab.</span></span>
4. <span data-ttu-id="c070d-150">**영어(미국)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-150">Click **English (US)**.</span></span>
5. <span data-ttu-id="c070d-151">Hello 클릭 **세부 정보** 탭 합니다. Hello에 **설명** 섹션, 업데이트에서 hello 제공 **제목**, **요약**, 및 **세부 요약** hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-151">Click hello **DETAILS** tab. In hello **Description** section, update hello offer **TITLE**, **SUMMARY**, and **LONG SUMMARY** and save hello changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c070d-152">Hello SKU 세부 정보를 업데이트할 때 이러한 제한 사항을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-152">When you update hello SKU details, be aware of these restrictions:</span></span> 
   * <span data-ttu-id="c070d-153">Hello 서비스 설명 및 hello SKU 설명에 대 한 중복 텍스트를 입력 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-153">Do not enter duplicate text for hello offer description and hello SKU description.</span></span>
   * <span data-ttu-id="c070d-154">Hello SKU 제목과 hello 제공 긴 요약에 대 한 중복 텍스트를 입력 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-154">Do not enter duplicate text for hello SKU title and hello offer long summary.</span></span> 
   * <span data-ttu-id="c070d-155">Hello SKU 제목과 hello 제공 요약에 대 한 중복 텍스트를 입력 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-155">Do not enter duplicate text for hello SKU title and hello offer summary.</span></span>
   >
   >

    ![세부 정보](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. <span data-ttu-id="c070d-157">Hello에 **로고** hello 섹션 **세부 정보** 탭, hello 로고를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-157">In hello **LOGOS** section of hello **DETAILS** tab, update hello logos.</span></span> <span data-ttu-id="c070d-158">Hello 로고 hello 따라야 [Azure 마켓플레이스 지침](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-158">Ensure that hello logos follow hello [Azure Marketplace guidelines](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>

   > [!NOTE]
   > <span data-ttu-id="c070d-159">대표 아이콘은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-159">A hero icon is optional.</span></span> <span data-ttu-id="c070d-160">Hero 아이콘 하지 tooupload를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-160">You can choose not tooupload a hero icon.</span></span> <span data-ttu-id="c070d-161">그러나 hero 아이콘을 업로드 한 후이 없는 프로 비전 toodelete hello에서 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-161">However, after a hero icon is uploaded, there is no provision toodelete it from hello Publishing portal.</span></span> <span data-ttu-id="c070d-162">Hello에 따라 [hero 아이콘 지침](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-162">Follow hello [hero icon guidelines](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>
   >
   >
7. <span data-ttu-id="c070d-163">Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-163">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="c070d-164">참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-164">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="c070d-165">제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-165">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-166">클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-166">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![로고](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a><span data-ttu-id="c070d-168">업데이트 hello SKU 설명</span><span class="sxs-lookup"><span data-stu-id="c070d-168">Update hello SKU description</span></span>
<span data-ttu-id="c070d-169">SKU에 자세히 설명 하 고 자신의 구독을 다시 게시 tooupdate hello 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-169">tooupdate hello SKU details and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="c070d-170">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-170">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="c070d-171">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-171">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-172">Hello hello 왼쪽 메뉴를 클릭 hello **마케팅** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-172">In hello menu on hello left, click hello **MARKETING** tab.</span></span>
4. <span data-ttu-id="c070d-173">**영어(미국)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-173">Click **English (US)**.</span></span>
5. <span data-ttu-id="c070d-174">Hello 클릭 **계획** 탭 합니다. Hello에 **Sku** 섹션, SKU hello 업데이트 **제목**, **요약**, 및 **설명** hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-174">Click hello **PLANS** tab. In hello **SKUs** section, update hello SKU **TITLE**, **SUMMARY**, and **DESCRIPTION** and save hello changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c070d-175">Hello SKU 세부 정보를 업데이트할 때 이러한 제한 사항을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-175">When you update hello SKU details, be aware of these restrictions:</span></span> 
   * <span data-ttu-id="c070d-176">Hello 서비스 설명 및 hello SKU 설명에 대 한 중복 텍스트를 입력 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-176">Do not enter duplicate text for hello offer description and hello SKU description.</span></span> 
   * <span data-ttu-id="c070d-177">Hello SKU 제목과 hello 제공 긴 요약에 대 한 중복 텍스트를 입력 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-177">Do not enter duplicate text for hello SKU title and hello offer long summary.</span></span> 
   * <span data-ttu-id="c070d-178">Hello SKU 제목과 hello 제공 요약에 대 한 중복 텍스트를 입력 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-178">Do not enter duplicate text for hello SKU title and hello offer summary.</span></span>
   >
   >
6. <span data-ttu-id="c070d-179">Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-179">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="c070d-180">참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-180">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="c070d-181">제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-181">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-182">클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-182">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![요금제](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a><span data-ttu-id="c070d-184">기존 링크 변경 또는 새 링크 추가</span><span class="sxs-lookup"><span data-stu-id="c070d-184">Change existing links or add new links</span></span>
<span data-ttu-id="c070d-185">toochange 기존 연결 또는 새 링크를 추가 하 고 제안을 다시 게시 한 다음, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-185">toochange existing links or add new links and then republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="c070d-186">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-186">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="c070d-187">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-187">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-188">Hello hello 왼쪽 메뉴를 클릭 hello **마케팅** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-188">In hello menu on hello left, click hello **MARKETING** tab.</span></span>
4. <span data-ttu-id="c070d-189">**영어(미국)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-189">Click **English (US)**.</span></span>
5. <span data-ttu-id="c070d-190">Hello 클릭 **링크** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-190">Click hello **LINKS** tab.</span></span>
6. <span data-ttu-id="c070d-191">새 링크를 hello tooadd **링크** 섹션에서 클릭 **+ 링크 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-191">tooadd a new link, in hello **Links** section, click **+ ADD LINK**.</span></span> <span data-ttu-id="c070d-192">Hello에 **링크 추가** 대화 상자에서 hello 링크 입력 **제목** 및 **URL** hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-192">In hello **Add Link** dialog box, enter hello link **TITLE** and **URL** and save hello changes.</span></span> <span data-ttu-id="c070d-193">고객에게 도움이 될 수 있는 정보를 포함하는 모든 링크를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-193">You can enter any link that contains information that might help customers.</span></span>
7. <span data-ttu-id="c070d-194">hello 링크를 선택 하 고 hello 클릭 tooupdate 또는 기존 링크를 삭제 **편집** 단추나 hello **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-194">tooupdate or delete an existing link, select hello link and click hello **Edit** button or hello **Delete** button.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c070d-195">이러한 링크 프로덕션 요청 프로세스 중에 유효성이 검사 가져오기 때문에이 섹션에 입력 한 hello 링크가 제대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-195">Ensure that hello links that you've entered in this section are working properly, because these links get validated during your production request process.</span></span>
   >
   >
8. <span data-ttu-id="c070d-196">Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-196">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="c070d-197">참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-197">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
9. <span data-ttu-id="c070d-198">제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-198">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-199">클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-199">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![링크](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![링크 추가](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a><span data-ttu-id="c070d-202">기존 샘플 이미지 변경 또는 새 샘플 이미지 추가</span><span class="sxs-lookup"><span data-stu-id="c070d-202">Change an existing sample image or add a new sample image</span></span>
<span data-ttu-id="c070d-203">기존 샘플 toochange 이미지 또는 새 샘플 이미지를 추가 하 고 다음 제안을 다시 게시, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-203">toochange an existing sample image or add new sample images and then republish your offer, follow these steps:</span></span>

> [!NOTE]
> <span data-ttu-id="c070d-204">Hello에 하나의 샘플 이미지가 표시 되어 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-204">Only one sample image is displayed in hello [Azure portal](https://portal.azure.com).</span></span>
>
>

1. <span data-ttu-id="c070d-205">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-205">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="c070d-206">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-206">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-207">Hello hello 왼쪽 메뉴를 클릭 hello **마케팅** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-207">In hello menu on hello left, click hello **MARKETING** tab.</span></span>
4. <span data-ttu-id="c070d-208">**영어(미국)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-208">Click **English (US)**.</span></span>
5. <span data-ttu-id="c070d-209">Hello 클릭 **샘플 이미지가** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-209">Click hello **SAMPLE IMAGES** tab.</span></span>
6. <span data-ttu-id="c070d-210">tooadd hello에서 새 샘플 이미지 **샘플 이미지** 섹션에서 클릭 **새 이미지 업로드** hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-210">tooadd a new sample image, in hello **Sample Images** section, click **UPLOAD A NEW IMAGE** and save hello changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c070d-211">샘플 이미지를 포함하는 것은 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-211">Including a sample image is optional.</span></span>
   >
7. <span data-ttu-id="c070d-212">Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-212">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="c070d-213">참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-213">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="c070d-214">제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-214">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-215">클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-215">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![샘플 이미지](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a><span data-ttu-id="c070d-217">Hello 법적 콘텐츠 업데이트</span><span class="sxs-lookup"><span data-stu-id="c070d-217">Update hello legal content</span></span>
<span data-ttu-id="c070d-218">tooupdate 법적 콘텐츠 hello 및 제안을 다시 게시, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-218">tooupdate hello legal content and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="c070d-219">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-219">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="c070d-220">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-220">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-221">Hello hello 왼쪽 메뉴를 클릭 hello **마케팅** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-221">In hello menu on hello left, click hello **MARKETING** tab.</span></span>
4. <span data-ttu-id="c070d-222">**영어(미국)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-222">Click **English (US)**.</span></span>
5. <span data-ttu-id="c070d-223">Hello 클릭 **법적** 탭 합니다. Hello에 **법적** 섹션에서 사용자 정책/사용 약관을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-223">Click hello **LEGAL** tab. In hello **Legal** section, update your policies/terms of use.</span></span> <span data-ttu-id="c070d-224">입력 하거나 hello 정책/조건 hello에 붙여 **사용 약관** 상자 고 hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-224">Enter or paste hello policies/terms in hello **TERMS OF USE** box and save hello changes.</span></span>
6. <span data-ttu-id="c070d-225">사용 약관 hello에 대 한 hello 문자 제한 길이 1 백만 자 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-225">hello character limit for hello legal terms of use is 1 million characters.</span></span>
7. <span data-ttu-id="c070d-226">Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-226">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="c070d-227">참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-227">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="c070d-228">제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-228">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-229">클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-229">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![법적 정보](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a><span data-ttu-id="c070d-231">Hello 지원 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-231">Update hello support information</span></span>
<span data-ttu-id="c070d-232">tooupdate hello 지원 정보 및 제안 다시 게시 하 고, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-232">tooupdate hello support information and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="c070d-233">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-233">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="c070d-234">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-234">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-235">Hello hello 왼쪽 메뉴를 클릭 hello **지원** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-235">In hello menu on hello left, click hello **SUPPORT** tab.</span></span>
4. <span data-ttu-id="c070d-236">Hello에 **엔지니어링 문의** 섹션 업데이트 hello 엔지니어링 연락처 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-236">In hello **Engineering Contact** section, update hello engineering contact details.</span></span> <span data-ttu-id="c070d-237">이러한 세부 정보는만 hello 파트너와 Microsoft 간의 내부 통신에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-237">These details are used for internal communication between hello partner and Microsoft only.</span></span>
5. <span data-ttu-id="c070d-238">Hello에 **고객 지원 서비스** 섹션에서 업데이트 hello 지원 연락처 정보 및 hello **지원 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-238">In hello **Customer Support** section, update hello support contact details and hello **SUPPORT URL**.</span></span> <span data-ttu-id="c070d-239">이러한 세부 정보는만 hello 파트너와 Microsoft 간의 내부 통신에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-239">These details are used for internal communication between hello partner and Microsoft only.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c070d-240">Tooprovide만 전자 메일 지원을 원하는 경우 hello에 더미 전화 번호를 입력 **고객 지원 서비스** 섹션.</span><span class="sxs-lookup"><span data-stu-id="c070d-240">If you want tooprovide only email support, enter a dummy phone number in hello **Customer Support** section.</span></span> <span data-ttu-id="c070d-241">이 경우 사용자가 제공한 hello 전자 메일을 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-241">In this case, hello email you provided is used instead.</span></span>
   >
   >
6. <span data-ttu-id="c070d-242">Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-242">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="c070d-243">참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-243">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="c070d-244">제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-244">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-245">클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-245">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![지원](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a><span data-ttu-id="c070d-247">업데이트 hello 범주</span><span class="sxs-lookup"><span data-stu-id="c070d-247">Update hello categories</span></span>
<span data-ttu-id="c070d-248">범주 제안에 대 한 섹션 및 제품을 다시 게시 tooupdate hello 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-248">tooupdate hello categories section for your offer and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="c070d-249">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-249">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="c070d-250">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-250">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-251">Hello hello 왼쪽 메뉴를 클릭 hello **범주** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-251">In hello menu on hello left, click hello **CATEGORIES** tab.</span></span>
4. <span data-ttu-id="c070d-252">Hello에 **범주** 섹션, 자신의 구독에 대 한 hello 범주를 업데이트 하 고, hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-252">In hello **Categories** section, update hello categories for your offer and save hello changes.</span></span> <span data-ttu-id="c070d-253">Hello Azure 마켓플레이스 갤러리에 대 한 toofive 범주를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-253">You can choose up toofive categories for hello Azure Marketplace gallery.</span></span>
5. <span data-ttu-id="c070d-254">Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-254">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="c070d-255">참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-255">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
6. <span data-ttu-id="c070d-256">제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-256">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-257">클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-257">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![범주](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a><span data-ttu-id="c070d-259">나열된 제품에 새 SKU 추가</span><span class="sxs-lookup"><span data-stu-id="c070d-259">Add a new SKU under a listed offer</span></span>
<span data-ttu-id="c070d-260">라이브 해당 제품에 대 한 새로운 SKU tooadd 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-260">tooadd a new SKU in your live offer, follow these steps:</span></span>

1. <span data-ttu-id="c070d-261">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-261">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="c070d-262">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-262">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-263">Hello hello 왼쪽 메뉴를 클릭 hello **SKU** 탭 합니다. 그런 다음 **SKU 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-263">In hello menu on hello left, click hello **SKUS** tab. Then click **Add a SKU**.</span></span> 
4. <span data-ttu-id="c070d-264">Hello 대화 상자에서 입력 한 **SKU 식별자** 소문자로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-264">In hello dialog box, enter a **SKU Identifier** in lowercase.</span></span> <span data-ttu-id="c070d-265">선택 hello **라이선스 (BYOL) 청구 모델에 고유한** 확인란 toopublish 선택 hello 새로운 SKU BYOL 청구 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-265">Select hello **Bring your own license (BYOL) billing model** check box if you want toopublish hello new SKU with a BYOL billing model.</span></span> <span data-ttu-id="c070d-266">그렇지 않으면 hello 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-266">Otherwise, clear hello check box.</span></span> <span data-ttu-id="c070d-267">Hello 눈금 표시가 toocreate 새로운 SKU를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-267">Click hello tick mark toocreate a new SKU.</span></span> <span data-ttu-id="c070d-268">Hello BYOL 청구 모델을 선택 하지 않은 hello 청구 모델 toohourly 자동 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-268">If you didn't choose hello BYOL billing model, hello billing model is automatically set toohourly.</span></span> <span data-ttu-id="c070d-269">Hello 시간별 요금 청구 모델에 대 한 hello 30 일 무료 평가판 선택 **ׁ ´ ** 에 대 한 **무료 평가판을 사용할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="c070d-269">If you want hello 30-day free trial for hello hourly billing model, select **One Month** for **Is a free trial available?**</span></span> <span data-ttu-id="c070d-270">그렇지 않은 경우 **평가판 없음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-270">Otherwise, select **No Trial**.</span></span> <span data-ttu-id="c070d-271">(**무료 평가판을 사용할 수 있는?**  새로운 SKU hello를 만드는 동안 BYOL 선택 하지 않은 경우에 나타납니다.)</span><span class="sxs-lookup"><span data-stu-id="c070d-271">(**Is a free trial available?** appears only if you haven't selected BYOL while creating hello new SKU.)</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c070d-272">**솔루션 템플릿을 통해 항상 구입 해야 하기 때문에이 SKU hello Marketplace에서에서 숨기기** 해야 **예** *만* 솔루션 템플릿을 게시 하기 위한 승인 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c070d-272">**Hide this SKU from hello Marketplace because it should always be bought via a solution template** should be **Yes** *only* if you're approved for publishing a solution template.</span></span> <span data-ttu-id="c070d-273">그렇지 않은 경우 이 옵션은 항상 **아니요**로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-273">Otherwise, this option should always be **No**.</span></span>
   >
   >
4. <span data-ttu-id="c070d-274">Hello hello 왼쪽 메뉴를 클릭 hello **VM 이미지** 탭과 확인 hello 사용자가 만든 새로운 SKU입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-274">In hello menu on hello left, click hello **VM IMAGES** tab and find out hello new SKU that you've created.</span></span>
5. <span data-ttu-id="c070d-275">tooset 최대 새로운 SKU hello, 참조 [VM 이미지에 대 한 인증을 가져오는](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-275">tooset up hello new SKU, see [Obtain certification for your VM image](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) for guidance.</span></span>
6. <span data-ttu-id="c070d-276">tooadd 마케팅 자료에 대 한 새로운 SKU hello, 참조 [마케팅 콘텐츠 제공 마켓플레이스](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-276">tooadd marketing material for hello new SKU, see [Provide Marketplace marketing content](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>
7. <span data-ttu-id="c070d-277">tooadd 가격 정보에 대 한 새로운 SKU hello, 참조 [가격 설정](marketplace-publishing-push-to-staging.md#step-2-set-your-prices)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-277">tooadd pricing information for hello new SKU, see [Set your prices](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).</span></span>
8. <span data-ttu-id="c070d-278">Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-278">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="c070d-279">참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-279">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
9. <span data-ttu-id="c070d-280">제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-280">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-281">클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-281">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![SKU 추가](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a><span data-ttu-id="c070d-284">나열 된 SKU에 대 한 hello 데이터 디스크 개수 변경</span><span class="sxs-lookup"><span data-stu-id="c070d-284">Change hello data disk count for a listed SKU</span></span>
<span data-ttu-id="c070d-285">있습니다 수 증가/감소 나열 된 SKU의 hello 데이터 디스크 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-285">You can't increment/decrement hello data disk count of a listed SKU.</span></span> <span data-ttu-id="c070d-286">이 경우 새로운 SKU toocreate가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-286">You need toocreate a new SKU in this case.</span></span> <span data-ttu-id="c070d-287">자세한 지침은 toohello 섹션을 참조 하십시오. [아래 나열 된 제품은 새로운 SKU 추가](#add-a-new-sku-under-a-listed-offer)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-287">For detailed guidance, refer toohello section [Add a new SKU under a listed offer](#add-a-new-sku-under-a-listed-offer).</span></span>

## <a name="delete-a-listed-offer-from-hello-marketplace"></a><span data-ttu-id="c070d-288">Hello Marketplace에서에서 나열 된 제안을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-288">Delete a listed offer from hello Marketplace</span></span>
<span data-ttu-id="c070d-289">다양 한 측면 toobe 요청 tooremove 라이브 제품의 hello 경우에서 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-289">Various aspects need toobe taken care of in hello case of a request tooremove a live offer.</span></span> <span data-ttu-id="c070d-290">다음이 단계를 수행 하는 hello 지원 팀 tooremove hello Marketplace에서에서 나열 된 제품의에서 tooget 지침:</span><span class="sxs-lookup"><span data-stu-id="c070d-290">tooget guidance from hello support team tooremove a listed offer from hello Marketplace, follow these steps:</span></span>

1. <span data-ttu-id="c070d-291">Hello에 지원 티켓을 발생 시키는 [인시던트를 만들](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) 페이지.</span><span class="sxs-lookup"><span data-stu-id="c070d-291">Raise a support ticket on hello [Create an incident](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) page.</span></span>

2. <span data-ttu-id="c070d-292">**제품 관리**로 **문제 형식**을 선택하고 **프로덕션 환경에서 제품 및/또는 SKU 수정**으로 **범주**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-292">Select **Problem type** as **Managing offers**, and select **Category** as **Modifying an offer and/or SKU already in production**.</span></span>
3. <span data-ttu-id="c070d-293">Hello 요청을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-293">Submit hello request.</span></span>

<span data-ttu-id="c070d-294">hello 지원 팀 hello 제공/SKU 삭제 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-294">hello support team guides you through hello offer/SKU deletion process.</span></span>

> [!NOTE]
> <span data-ttu-id="c070d-295">초안 상태 (하지만 준비 또는 프로덕션) 되는 동안 항상 hello 제공을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-295">You can always delete hello offer while it is in Draft status (but not Staging or Production).</span></span> <span data-ttu-id="c070d-296">Hello에 **기록** 탭을 클릭 **초안 버리기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-296">On hello **HISTORY** tab, click **DISCARD DRAFT**.</span></span>
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a><span data-ttu-id="c070d-297">Hello Marketplace에서에서 나열 된 SKU를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-297">Delete a listed SKU from hello Marketplace</span></span>
<span data-ttu-id="c070d-298">toodelete hello Marketplace에서에서 나열 된 SKU는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-298">toodelete a listed SKU from hello Marketplace, follow these steps:</span></span>

1. <span data-ttu-id="c070d-299">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-299">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="c070d-300">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-300">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-301">Hello hello 왼쪽 창에서 클릭 hello **SKU** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-301">In hello pane on hello left, click hello **SKUS** tab.</span></span>
4. <span data-ttu-id="c070d-302">선택 hello SKU toodelete, 원하고 hello 클릭 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-302">Select hello SKU that you want toodelete, and click hello **Delete** button.</span></span>
5. <span data-ttu-id="c070d-303">Toohello 이동 **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-303">Go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-304">클릭 **요청 승인 tooPUSH tooPRODUCTION** hello Marketplace에서에서 toorepublish hello 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-304">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish hello offer in hello Marketplace.</span></span>
6. <span data-ttu-id="c070d-305">Hello 제품은 시장 hello에 다시 게시 하면 hello SKU 마켓플레이스 hello 및 hello Azure 포털에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-305">After hello offer is republished in hello Marketplace, hello SKU is deleted from hello Marketplace and hello Azure portal.</span></span>

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a><span data-ttu-id="c070d-306">Hello Marketplace에서에서 나열 된 SKU의 hello 현재 버전을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-306">Delete hello current version of a listed SKU from hello Marketplace</span></span>
<span data-ttu-id="c070d-307">다음이 단계를 수행 하는 hello toodelete hello Marketplace에서에서 나열 된 SKU의 현재 버전:</span><span class="sxs-lookup"><span data-stu-id="c070d-307">toodelete hello current version of a listed SKU from hello Marketplace, follow these steps:</span></span> 

1. <span data-ttu-id="c070d-308">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-308">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="c070d-309">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-309">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-310">Hello hello 왼쪽 메뉴를 클릭 hello **VM 이미지** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-310">In hello menu on hello left, click hello **VM IMAGES** tab.</span></span>
4. <span data-ttu-id="c070d-311">인 현재 SKU hello 선택 버전 hello 누르고 toodelete, 원하는 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-311">Select hello SKU whose current version you want toodelete, and click hello **Delete** button.</span></span>
5. <span data-ttu-id="c070d-312">Toohello 이동 **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-312">Go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-313">클릭 **요청 승인 tooPUSH tooPRODUCTION** hello Marketplace에서에서 toorepublish hello 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-313">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish hello offer in hello Marketplace.</span></span>
6. <span data-ttu-id="c070d-314">Hello 제안을 가져옵니다 hello Marketplace에에서 다시 게시 하면 후 hello 현재 버전의 hello 나열 된 SKU hello 마켓플레이스와 hello Azure 포털에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-314">After hello offer gets republished in hello Marketplace, hello current version of hello listed SKU is deleted from hello Marketplace and hello Azure portal.</span></span> <span data-ttu-id="c070d-315">hello SKU 다음 롤백됩니다 tooits 이전 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-315">hello SKU is then rolled back tooits previous version.</span></span>

## <a name="revert-hello-listing-price-tooproduction-values"></a><span data-ttu-id="c070d-316">가격 tooproduction 값을 나열 하는 hello 되돌리기</span><span class="sxs-lookup"><span data-stu-id="c070d-316">Revert hello listing price tooproduction values</span></span>
<span data-ttu-id="c070d-317">toorevert hello 목록 가격 tooproduction 값 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-317">toorevert hello listing price tooproduction values, follow these steps:</span></span>

1. <span data-ttu-id="c070d-318">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-318">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="c070d-319">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-319">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-320">Hello hello 왼쪽 메뉴를 클릭 hello **가격 책정** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-320">In hello menu on hello left, click hello **PRICING** tab.</span></span>
4. <span data-ttu-id="c070d-321">가격 원하는 지역을 선택 tooreset 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-321">Select a region whose pricing you want tooreset.</span></span>

    ![가격 책정 지역](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. <span data-ttu-id="c070d-323">Sku 시간별 요금 청구 모델에 대 한 hello 선택한 영역에 대 한 프로덕션에 있는 것 처럼 모든 hello 코어에 대 한 hello 가격 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-323">For SKUs with an hourly billing model, reset hello prices for all hello cores as they are in production for hello selected region.</span></span> <span data-ttu-id="c070d-324">BYOL 청구 모델에 대 한 Sku, 확인 hello hello hello SKU에 대 한 확인란을 선택 하 여 hello 지역에서 사용할 수 있는 SKU hello **EXTERNALLY-LICENSED (BYOL) SKU 가용성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="c070d-324">For SKUs with a BYOL billing model, make hello SKU available in hello region by selecting hello check box for hello SKU in hello **EXTERNALLY-LICENSED (BYOL) SKU AVAILABILITY** section.</span></span>

    ![가격 책정 모델](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. <span data-ttu-id="c070d-326">**미국의 가격에 따라 다른 마켓의 가격 자동 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-326">Click **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c070d-327">hello 단추의 레이블을 선택 하는 hello 지역에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-327">hello button’s label might be different depending on hello region that you select.</span></span> <span data-ttu-id="c070d-328">미국을 선택 하는 것 때문에 hello 단추인 **AUTOPRICE 다른 시장 기반 ON 가격 IN 통합 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-328">Because we selected United States, hello button is labeled **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES**.</span></span>
   >
   >

    ![가격 자동 설정](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. <span data-ttu-id="c070d-330">에 hello Autoprice 마법사의 1 페이지 hello 기본 시장을 선택 하 고 hello 클릭 **화살표** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-330">On page 1 of hello Autoprice wizard, choose hello base market and click hello **arrow** button.</span></span>

    ![기본 시장](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. <span data-ttu-id="c070d-332">2 페이지 서비스 계획과 미터 (코어)를 선택 하 고 hello 클릭 **화살표** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-332">On page 2, choose service plans and meters (cores), and click hello **arrow** button.</span></span>

    ![서비스 계획 및 미터](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. <span data-ttu-id="c070d-334">3 페이지 클릭 **토글 모든** tooselect 모든 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-334">On page 3, click **Toggle All** tooselect all regions.</span></span> <span data-ttu-id="c070d-335">또는 특정 지역에 대한 확인란을 수동으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-335">Or you can manually select check boxes for specific regions.</span></span> <span data-ttu-id="c070d-336">Hello 클릭 **화살표** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-336">Click hello **arrow** button.</span></span>

    ![시장 선택](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. <span data-ttu-id="c070d-338">4 페이지 hello 환율을 검토 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-338">On page 4, review hello exchange rates and click **Finish**.</span></span> <span data-ttu-id="c070d-339">hello 마법사 tooyour 선택 항목에 따라 가격 hello를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-339">hello wizard resets hello pricing according tooyour selections.</span></span>

11. <span data-ttu-id="c070d-340">Hello에 **가격 책정** 탭을 클릭 **보기 및 변경 내용 요약**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-340">On hello **PRICING** tab, click **VIEW SUMMARY AND CHANGES**.</span></span>
    <span data-ttu-id="c070d-341">**버전 보기**에서 **초안**을 선택하고 **비교 대상**에서 **프로덕션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-341">For **View Version**, select **Draft**, and for **Compare with**, select **Production**.</span></span> <span data-ttu-id="c070d-342">가격 책정 차이점이 표시 되 면 hello 가격 되돌릴 toohello 프로덕션 값 성공적으로.</span><span class="sxs-lookup"><span data-stu-id="c070d-342">If you see no pricing difference, hello pricing reverted toohello production values successfully.</span></span>

    ![요약 및 변경 내용 보기](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. <span data-ttu-id="c070d-344">Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-344">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="c070d-345">참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-345">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
13. <span data-ttu-id="c070d-346">제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-346">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-347">클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-347">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

## <a name="revert-hello-billing-model-tooproduction-values"></a><span data-ttu-id="c070d-348">청구 모델 tooproduction 값 hello 되돌리기</span><span class="sxs-lookup"><span data-stu-id="c070d-348">Revert hello billing model tooproduction values</span></span>
<span data-ttu-id="c070d-349">toorevert hello 청구 모델 tooproduction 값을 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="c070d-349">toorevert hello billing model tooproduction values, follow these steps:</span></span>

1. <span data-ttu-id="c070d-350">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-350">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="c070d-351">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-351">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-352">Hello hello 왼쪽 메뉴를 클릭 hello **SKU** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-352">In hello menu on hello left, click hello **SKUS** tab.</span></span>
4. <span data-ttu-id="c070d-353">Hello 클릭 **편집** 단추 toorevert hello에 대 한 청구 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-353">Click hello **Edit** button toorevert hello billing model.</span></span> <span data-ttu-id="c070d-354">Hello 창이 열리면을 늘리거나 hello **대금 청구 및 라이선스 (즉, Bring Your 자체 라이선스) Azure에서 외부에서 수행 되** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-354">In hello window that opens, select or clear hello **Billing and licensing is done externally from Azure (aka Bring Your Own License)** check box.</span></span>

    ![청구 편집](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. <span data-ttu-id="c070d-356">이 문서의 "Revert hello 가격 tooproduction 값 나열 하 는" hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-356">Follow hello steps in "Revert hello listing price tooproduction values" in this article.</span></span>
6. <span data-ttu-id="c070d-357">Toohello 이동 **게시** 탭을 클릭 **푸시 tooSTAGING**합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-357">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="c070d-358">참조에 대 한 자세한 지침은 제안을 hello 스테이징 환경에서에서 테스트, [마켓플레이스 hello에 대 한 VM 제안을 테스트](marketplace-publishing-vm-image-test-in-staging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-358">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="c070d-359">제안을 테스트 한 후 스테이징 이동 toohello **게시** 탭 hello에 포털을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-359">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="c070d-360">클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-360">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a><span data-ttu-id="c070d-361">나열 된 SKU toohello 프로덕션 값의 표시 유형 설정 hello 되돌리기</span><span class="sxs-lookup"><span data-stu-id="c070d-361">Revert hello visibility setting of a listed SKU toohello production value</span></span>
<span data-ttu-id="c070d-362">다음이 단계를 수행 하는 나열 된 SKU toohello 프로덕션 값의 toorevert hello 표시 유형을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-362">toorevert hello visibility setting of a listed SKU toohello production value, follow these steps:</span></span>

1. <span data-ttu-id="c070d-363">Toohello 로그인 [게시 포털](https://publish.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-363">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="c070d-364">Toohello 이동 **가상 컴퓨터** 탭을 자신의 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-364">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="c070d-365">Hello hello 왼쪽 메뉴를 클릭 hello **SKU** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-365">In hello menu on hello left, click hello **SKUS** tab.</span></span>
4. <span data-ttu-id="c070d-366">SKU을 선택 하 고 hello SKU toohello 프로덕션 값의 표시 유형을 설정 hello를 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-366">Select your SKU, and revert hello visibility setting of hello SKU toohello production value.</span></span>

    ![표시 유형](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. <span data-ttu-id="c070d-368">Hello 변경을 마친 후 클릭 **요청 승인 tooPUSH tooPRODUCTION** toorepublish hello Marketplace에서에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c070d-368">After you're done with hello changes, click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

## <a name="see-also"></a><span data-ttu-id="c070d-369">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c070d-369">See also</span></span>
* [<span data-ttu-id="c070d-370">시작: 제안 toohello Azure 마켓플레이스에서 게시</span><span class="sxs-lookup"><span data-stu-id="c070d-370">Get Started: Publish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="c070d-371">지급 보고 이해</span><span class="sxs-lookup"><span data-stu-id="c070d-371">Understand payout reporting</span></span>](marketplace-publishing-report-payout.md)
* [<span data-ttu-id="c070d-372">클라우드 솔루션 공급자 재판매인 인센티브 변경</span><span class="sxs-lookup"><span data-stu-id="c070d-372">Change your Cloud Solution Provider reseller incentive</span></span>](marketplace-publishing-csp-incentive.md)
* [<span data-ttu-id="c070d-373">Hello Marketplace에서에서 일반적인 게시 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c070d-373">Troubleshoot common publishing problems in hello Marketplace</span></span>](marketplace-publishing-support-common-issues.md)
* [<span data-ttu-id="c070d-374">게시자로 지원 받기</span><span class="sxs-lookup"><span data-stu-id="c070d-374">Get support as a publisher</span></span>](marketplace-publishing-get-publisher-support.md)
* [<span data-ttu-id="c070d-375">온-프레미스 VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="c070d-375">Create a VM image on-premises</span></span>](marketplace-publishing-vm-image-creation-on-premise.md)
* [<span data-ttu-id="c070d-376">Hello Azure 미리 보기 포털에서 Windows를 실행 하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="c070d-376">Create a virtual machine running Windows in hello Azure preview portal</span></span>](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

---
title: "Azure Marketplace에서 가상 컴퓨터 이미지 관리 | Microsoft Docs"
description: "초기 게시 후 Azure Marketplace에서 가상 컴퓨터 이미지를 관리하는 방법에 대한 자세한 가이드입니다."
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
ms.openlocfilehash: e1f90650e71345957c2d353774cb8bef62c1868b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-the-azure-marketplace"></a><span data-ttu-id="f92ce-103">Azure 마켓플레이스의 가상 컴퓨터 제품에 대한 프로덕션 이후 가이드</span><span class="sxs-lookup"><span data-stu-id="f92ce-103">Post-production guide for virtual machine offers in the Azure Marketplace</span></span>
<span data-ttu-id="f92ce-104">이 문서에서는 Azure Marketplace의 라이브 가상 컴퓨터 제품을 업데이트하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-104">This article explains how you can update a live virtual machine offer in the Azure Marketplace.</span></span> <span data-ttu-id="f92ce-105">기존 제품에 하나 이상의 새로운 SKU를 추가하는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-105">It guides you through the process of adding one or more new SKUs to an existing offer.</span></span> <span data-ttu-id="f92ce-106">또한 Marketplace에서 라이브 가상 컴퓨터 제품 또는 SKU를 제거하는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-106">It also guides you through the process of removing a live virtual machine offer or SKU from the Marketplace.</span></span>

<span data-ttu-id="f92ce-107">제품/SKU가 [Azure Portal](http://portal.azure.com)에서 준비된 후에는 다음과 같은 텍스트 상자를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-107">After an offer/SKU is staged in the [Azure portal](http://portal.azure.com), you can't change the following text boxes:</span></span>

* <span data-ttu-id="f92ce-108">**제품 식별자:** [게시 포털]에서 **가상 컴퓨터**로 이동하여 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-108">**Offer Identifier**: In the Publishing portal, go to **virtual machines** and select your offer.</span></span> <span data-ttu-id="f92ce-109">**VM 이미지** > **제품 식별자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-109">Then click **VM IMAGES** > **Offer Identifier**.</span></span>
* <span data-ttu-id="f92ce-110">**SKU 식별자:** [게시 포털]에서 **가상 컴퓨터**로 이동하여 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-110">**SKU Identifier**: In the Publishing portal, go to **virtual machines** and select your offer.</span></span> <span data-ttu-id="f92ce-111">**SKU** > **SKU 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-111">Then click **SKUS** > **Add a SKU**.</span></span>
* <span data-ttu-id="f92ce-112">**게시자 네임스페이스:** [게시 포털]에서 **가상 컴퓨터** > **연습 탭** > **회사에 대한 정보 제공**("2단계 회사 등록" 참조) > **게시자 네임스페이스** > **네임스페이스**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-112">**Publisher Namespace**: In the Publishing portal, go to **virtual machines** > **Walkthrough** > **Tell Us About Your Company** (found under “Step 2 Register Your Company”) > **Publisher Namespace** > **Namespace**.</span></span>

<span data-ttu-id="f92ce-113">제품/SKU가 [Marketplace](http://azure.microsoft.com/marketplace)에서 나열된 후에는 다음과 같은 텍스트 상자를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-113">After the offer/SKU is listed in the [Marketplace](http://azure.microsoft.com/marketplace), you can't change the following text boxes:</span></span>

* <span data-ttu-id="f92ce-114">**제품 식별자:** [게시 포털]에서 **가상 컴퓨터**로 이동하여 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-114">**Offer Identifier**: In the Publishing portal, go to **virtual machines** and select your offer.</span></span> <span data-ttu-id="f92ce-115">**VM 이미지** > **제품 식별자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-115">Then click **VM IMAGES** > **Offer Identifier**.</span></span>
* <span data-ttu-id="f92ce-116">**SKU 식별자:** [게시 포털]에서 **가상 컴퓨터**로 이동하여 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-116">**SKU Identifier**: In the Publishing portal, go to **virtual machines** and select your offer.</span></span> <span data-ttu-id="f92ce-117">**SKU** > **SKU 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-117">Then click **SKUS** > **Add a SKU**.</span></span>
* <span data-ttu-id="f92ce-118">**게시자 네임스페이스:** [게시 포털]에서 **가상 컴퓨터** > **연습 탭** > **회사에 대한 정보 제공**("2단계 등록" 참조) > **게시자 네임스페이스** > **네임스페이스**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-118">**Publisher Namespace**: In the Publishing portal, go to **virtual machines** > **Walkthrough** > **Tell Us About Your Company** (found under "Step 2 Register") **Publisher Namespace** > **Namespace**.</span></span>
* <span data-ttu-id="f92ce-119">**포트:** [게시 포털]에서 **가상 컴퓨터**로 이동하여 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-119">**Ports**: In the Publishing portal, go to **virtual machines** and select your offer.</span></span> <span data-ttu-id="f92ce-120">**VM 이미지** > **포트 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-120">Then click **VM IMAGES** > **Open Ports**.</span></span>
* <span data-ttu-id="f92ce-121">**나열된 SKU의 가격 책정 변경**</span><span class="sxs-lookup"><span data-stu-id="f92ce-121">**Pricing change of listed SKU(s)**</span></span>
* <span data-ttu-id="f92ce-122">**나열된 SKU의 청구 모델 변경**</span><span class="sxs-lookup"><span data-stu-id="f92ce-122">**Billing model change of listed SKU(s)**</span></span>
* <span data-ttu-id="f92ce-123">**나열된 SKU의 청구 지역 제거**</span><span class="sxs-lookup"><span data-stu-id="f92ce-123">**Removal of billing regions of listed SKU(s)**</span></span>
* <span data-ttu-id="f92ce-124">**나열된 SKU의 데이터 디스크 수 변경**</span><span class="sxs-lookup"><span data-stu-id="f92ce-124">**Changing the data disk count of listed SKU(s)**</span></span>

## <a name="update-the-technical-details-of-a-sku"></a><span data-ttu-id="f92ce-125">SKU의 기술 세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="f92ce-125">Update the technical details of a SKU</span></span>
<span data-ttu-id="f92ce-126">나열된 SKU에 새 버전을 추가하고 제품을 다시 게시하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-126">To add a new version to the listed SKU and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-127">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-127">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="f92ce-128">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-128">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-129">왼쪽 메뉴에서 **VM 이미지** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-129">In the menu on the left, click the **VM IMAGES** tab.</span></span>
4. <span data-ttu-id="f92ce-130">**SKU** 섹션에서 업데이트하려는 SKU를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-130">In the **SKUs** section, locate the SKU that you want to update.</span></span>
5. <span data-ttu-id="f92ce-131">SKU의 새 버전 번호를 추가하고 **+** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-131">Add a new version number for the SKU, and click the **+** button.</span></span> <span data-ttu-id="f92ce-132">새 버전은 X.Y.Z 형식이어야 하며 여기서 X, Y, Z는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-132">The new version should be in an X.Y.Z format, where X, Y, and Z are integers.</span></span> <span data-ttu-id="f92ce-133">버전 변경은 증분되어야만 합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-133">Version changes should only be incremental.</span></span>
6. <span data-ttu-id="f92ce-134">**OS VHD URL** 상자에 운영 체제 VHD에 대해 만들어진 공유 액세스 서명 URI를 입력하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-134">In the **OS VHD URL** box, enter the shared access signature URI created for the operating system VHD and save the changes.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f92ce-135">나열된 SKU의 데이터 디스크 수를 늘리거나 줄일 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-135">You can't increment/decrement the data disk count of a listed SKU.</span></span> <span data-ttu-id="f92ce-136">이 경우 새로운 SKU를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-136">You need to create a new SKU in this case.</span></span> <span data-ttu-id="f92ce-137">자세한 지침은 [나열된 제품에 새 SKU 추가](#add-a-new-sku-under-a-listed-offer) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-137">For detailed guidance, refer to the section [Add a new SKU under a listed offer](#add-a-new-sku-under-a-listed-offer).</span></span>
   >
   >
7. <span data-ttu-id="f92ce-138">**게시** 탭으로 이동하고 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-138">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="f92ce-139">스테이징 환경에서 제품을 테스트하는 방법에 대한 자세한 지침은 [Marketplace에서 VM 제품 테스트](marketplace-publishing-vm-image-test-in-staging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-139">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="f92ce-140">준비 단계에서 제품을 테스트한 후에 게시 포털에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-140">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-141">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-141">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![VM 이미지](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-the-nontechnical-details-of-an-offer-or-a-sku"></a><span data-ttu-id="f92ce-143">제품 또는 SKU의 비기술적인 세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="f92ce-143">Update the nontechnical details of an offer or a SKU</span></span>
<span data-ttu-id="f92ce-144">Marketplace에서 라이브 제품 또는 SKU의 비기술적인(마케팅, 법률, 지원, 범주) 세부 정보를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-144">You can update the nontechnical (marketing, legal, support, categories) details of your live offer or SKU in the Marketplace.</span></span>

### <a name="update-the-offer-description-and-logos"></a><span data-ttu-id="f92ce-145">제품 설명 및 로고 업데이트</span><span class="sxs-lookup"><span data-stu-id="f92ce-145">Update the offer description and logos</span></span>
<span data-ttu-id="f92ce-146">세부 정보를 업데이트하고 제품을 다시 게시하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-146">To update the offer details and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-147">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-147">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="f92ce-148">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-148">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-149">왼쪽 메뉴에서 **마케팅** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-149">In the menu on the left, click the **MARKETING** tab.</span></span>
4. <span data-ttu-id="f92ce-150">**영어(미국)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-150">Click **English (US)**.</span></span>
5. <span data-ttu-id="f92ce-151">**세부 정보** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-151">Click the **DETAILS** tab.</span></span> <span data-ttu-id="f92ce-152">**설명** 섹션에서 제품 **제목**, **요약** 및 **긴 요약**을 업데이트하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-152">In the **Description** section, update the offer **TITLE**, **SUMMARY**, and **LONG SUMMARY** and save the changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f92ce-153">SKU 세부 정보를 업데이트할 때 이러한 제한 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-153">When you update the SKU details, be aware of these restrictions:</span></span> 
   * <span data-ttu-id="f92ce-154">제품 설명 및 SKU 설명에 중복 텍스트를 입력하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-154">Do not enter duplicate text for the offer description and the SKU description.</span></span>
   * <span data-ttu-id="f92ce-155">SKU 제목 및 제품 긴 요약에 중복 텍스트를 입력하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-155">Do not enter duplicate text for the SKU title and the offer long summary.</span></span> 
   * <span data-ttu-id="f92ce-156">SKU 제목 및 제품 요약에 중복 텍스트를 입력하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-156">Do not enter duplicate text for the SKU title and the offer summary.</span></span>
   >
   >

    ![세부 정보](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. <span data-ttu-id="f92ce-158">**세부 정보** 탭의 **로고** 섹션에서 로고를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-158">In the **LOGOS** section of the **DETAILS** tab, update the logos.</span></span> <span data-ttu-id="f92ce-159">로고가 [Azure Marketplace 지침](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)에 부합하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-159">Ensure that the logos follow the [Azure Marketplace guidelines](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>

   > [!NOTE]
   > <span data-ttu-id="f92ce-160">대표 아이콘은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-160">A hero icon is optional.</span></span> <span data-ttu-id="f92ce-161">대표 아이콘을 업로드하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-161">You can choose not to upload a hero icon.</span></span> <span data-ttu-id="f92ce-162">그러나 대표 아이콘을 업로드하면 게시 포털에서 삭제할 프로비전이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-162">However, after a hero icon is uploaded, there is no provision to delete it from the Publishing portal.</span></span> <span data-ttu-id="f92ce-163">[대표 아이콘 지침](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-163">Follow the [hero icon guidelines](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>
   >
   >
7. <span data-ttu-id="f92ce-164">**게시** 탭으로 이동하고 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-164">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="f92ce-165">스테이징 환경에서 제품을 테스트하는 방법에 대한 자세한 지침은 [Marketplace에서 VM 제품 테스트](marketplace-publishing-vm-image-test-in-staging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-165">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="f92ce-166">준비 단계에서 제품을 테스트한 후에 게시 포털에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-166">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-167">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-167">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![로고](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-the-sku-description"></a><span data-ttu-id="f92ce-169">SKU 설명 업데이트</span><span class="sxs-lookup"><span data-stu-id="f92ce-169">Update the SKU description</span></span>
<span data-ttu-id="f92ce-170">SKU 세부 정보를 업데이트하고 제품을 다시 게시하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-170">To update the SKU details and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-171">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-171">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="f92ce-172">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-172">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-173">왼쪽 메뉴에서 **마케팅** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-173">In the menu on the left, click the **MARKETING** tab.</span></span>
4. <span data-ttu-id="f92ce-174">**영어(미국)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-174">Click **English (US)**.</span></span>
5. <span data-ttu-id="f92ce-175">**계획** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-175">Click the **PLANS** tab.</span></span> <span data-ttu-id="f92ce-176">**SKU** 섹션에서 SKU **제목**, **요약** 및 **설명**을 업데이트하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-176">In the **SKUs** section, update the SKU **TITLE**, **SUMMARY**, and **DESCRIPTION** and save the changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f92ce-177">SKU 세부 정보를 업데이트할 때 이러한 제한 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-177">When you update the SKU details, be aware of these restrictions:</span></span> 
   * <span data-ttu-id="f92ce-178">제품 설명 및 SKU 설명에 중복 텍스트를 입력하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-178">Do not enter duplicate text for the offer description and the SKU description.</span></span> 
   * <span data-ttu-id="f92ce-179">SKU 제목 및 제품 긴 요약에 중복 텍스트를 입력하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-179">Do not enter duplicate text for the SKU title and the offer long summary.</span></span> 
   * <span data-ttu-id="f92ce-180">SKU 제목 및 제품 요약에 중복 텍스트를 입력하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-180">Do not enter duplicate text for the SKU title and the offer summary.</span></span>
   >
   >
6. <span data-ttu-id="f92ce-181">**게시** 탭으로 이동하고 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-181">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="f92ce-182">스테이징 환경에서 제품을 테스트하는 방법에 대한 자세한 지침은 [Marketplace에서 VM 제품 테스트](marketplace-publishing-vm-image-test-in-staging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-182">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="f92ce-183">준비 단계에서 제품을 테스트한 후에 게시 포털에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-183">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-184">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-184">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![요금제](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a><span data-ttu-id="f92ce-186">기존 링크 변경 또는 새 링크 추가</span><span class="sxs-lookup"><span data-stu-id="f92ce-186">Change existing links or add new links</span></span>
<span data-ttu-id="f92ce-187">기존 링크를 변경하거나 새 링크를 추가한 다음 제품을 다시 게시하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-187">To change existing links or add new links and then republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-188">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-188">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="f92ce-189">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-189">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-190">왼쪽 메뉴에서 **마케팅** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-190">In the menu on the left, click the **MARKETING** tab.</span></span>
4. <span data-ttu-id="f92ce-191">**영어(미국)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-191">Click **English (US)**.</span></span>
5. <span data-ttu-id="f92ce-192">**링크** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-192">Click the **LINKS** tab.</span></span>
6. <span data-ttu-id="f92ce-193">새 링크를 추가하려면 **링크** 섹션에서 **+ 링크 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-193">To add a new link, in the **Links** section, click **+ ADD LINK**.</span></span> <span data-ttu-id="f92ce-194">**링크 추가** 대화 상자에서 **제목** 및 **URL** 링크를 입력하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-194">In the **Add Link** dialog box, enter the link **TITLE** and **URL** and save the changes.</span></span> <span data-ttu-id="f92ce-195">고객에게 도움이 될 수 있는 정보를 포함하는 모든 링크를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-195">You can enter any link that contains information that might help customers.</span></span>
7. <span data-ttu-id="f92ce-196">기존 링크를 업데이트 또는 삭제하려면 링크를 선택하고 **편집** 단추 또는 **삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-196">To update or delete an existing link, select the link and click the **Edit** button or the **Delete** button.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f92ce-197">이러한 링크는 프로덕션 요청 프로세스 동안 유효성 검사를 받으므로 이 섹션에서 입력한 링크가 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-197">Ensure that the links that you've entered in this section are working properly, because these links get validated during your production request process.</span></span>
   >
   >
8. <span data-ttu-id="f92ce-198">**게시** 탭으로 이동하고 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-198">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="f92ce-199">스테이징 환경에서 제품을 테스트하는 방법에 대한 자세한 지침은 [Marketplace에서 VM 제품 테스트](marketplace-publishing-vm-image-test-in-staging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-199">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
9. <span data-ttu-id="f92ce-200">준비 단계에서 제품을 테스트한 후에 게시 포털에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-200">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-201">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-201">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![링크](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![링크 추가](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a><span data-ttu-id="f92ce-204">기존 샘플 이미지 변경 또는 새 샘플 이미지 추가</span><span class="sxs-lookup"><span data-stu-id="f92ce-204">Change an existing sample image or add a new sample image</span></span>
<span data-ttu-id="f92ce-205">기존 샘플 이미지를 변경하거나 새 샘플 이미지를 추가한 다음 제품을 다시 게시하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-205">To change an existing sample image or add new sample images and then republish your offer, follow these steps:</span></span>

> [!NOTE]
> <span data-ttu-id="f92ce-206">하나의 샘플 이미지만 [Azure Portal](https://portal.azure.com)에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-206">Only one sample image is displayed in the [Azure portal](https://portal.azure.com).</span></span>
>
>

1. <span data-ttu-id="f92ce-207">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-207">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="f92ce-208">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-208">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-209">왼쪽 메뉴에서 **마케팅** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-209">In the menu on the left, click the **MARKETING** tab.</span></span>
4. <span data-ttu-id="f92ce-210">**영어(미국)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-210">Click **English (US)**.</span></span>
5. <span data-ttu-id="f92ce-211">**샘플 이미지** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-211">Click the **SAMPLE IMAGES** tab.</span></span>
6. <span data-ttu-id="f92ce-212">새 샘플 이미지를 추가하려면 **샘플 이미지** 섹션에서 **새로운 이미지 업로드**를 클릭하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-212">To add a new sample image, in the **Sample Images** section, click **UPLOAD A NEW IMAGE** and save the changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f92ce-213">샘플 이미지를 포함하는 것은 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-213">Including a sample image is optional.</span></span>
   >
7. <span data-ttu-id="f92ce-214">**게시** 탭으로 이동하고 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-214">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="f92ce-215">스테이징 환경에서 제품을 테스트하는 방법에 대한 자세한 지침은 [Marketplace에서 VM 제품 테스트](marketplace-publishing-vm-image-test-in-staging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-215">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="f92ce-216">준비 단계에서 제품을 테스트한 후에 게시 포털에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-216">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-217">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-217">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![샘플 이미지](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-the-legal-content"></a><span data-ttu-id="f92ce-219">법적 콘텐츠 업데이트</span><span class="sxs-lookup"><span data-stu-id="f92ce-219">Update the legal content</span></span>
<span data-ttu-id="f92ce-220">법적 콘텐츠를 업데이트하고 제품을 다시 게시하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-220">To update the legal content and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-221">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-221">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="f92ce-222">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-222">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-223">왼쪽 메뉴에서 **마케팅** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-223">In the menu on the left, click the **MARKETING** tab.</span></span>
4. <span data-ttu-id="f92ce-224">**영어(미국)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-224">Click **English (US)**.</span></span>
5. <span data-ttu-id="f92ce-225">**법적** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-225">Click the **LEGAL** tab.</span></span> <span data-ttu-id="f92ce-226">**법적** 섹션 아래에서 정책/사용 약관을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-226">In the **Legal** section, update your policies/terms of use.</span></span> <span data-ttu-id="f92ce-227">**사용 약관** 텍스트 상자에 정책/용어를 입력하거나 붙여 넣고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-227">Enter or paste the policies/terms in the **TERMS OF USE** box and save the changes.</span></span>
6. <span data-ttu-id="f92ce-228">사용 약관의 문자 제한은 1백만자입니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-228">The character limit for the legal terms of use is 1 million characters.</span></span>
7. <span data-ttu-id="f92ce-229">**게시** 탭으로 이동하고 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-229">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="f92ce-230">스테이징 환경에서 제품을 테스트하는 방법에 대한 자세한 지침은 [Marketplace에서 VM 제품 테스트](marketplace-publishing-vm-image-test-in-staging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-230">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="f92ce-231">준비 단계에서 제품을 테스트한 후에 게시 포털에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-231">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-232">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-232">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![법적 정보](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-the-support-information"></a><span data-ttu-id="f92ce-234">지원 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="f92ce-234">Update the support information</span></span>
<span data-ttu-id="f92ce-235">지원 정보를 업데이트하고 제품을 다시 게시하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-235">To update the support information and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-236">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-236">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="f92ce-237">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-237">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-238">왼쪽 메뉴에서 **지원** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-238">In the menu on the left, click the **SUPPORT** tab.</span></span>
4. <span data-ttu-id="f92ce-239">**엔지니어링 문의** 섹션에서 엔지니어링 연락처 세부 정보를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-239">In the **Engineering Contact** section, update the engineering contact details.</span></span> <span data-ttu-id="f92ce-240">세부 정보는 파트너와 Microsoft 간의 내부 통신에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-240">These details are used for internal communication between the partner and Microsoft only.</span></span>
5. <span data-ttu-id="f92ce-241">**고객 지원** 섹션에서 지원 연락처 세부 정보 및 **지원 URL**을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-241">In the **Customer Support** section, update the support contact details and the **SUPPORT URL**.</span></span> <span data-ttu-id="f92ce-242">세부 정보는 파트너와 Microsoft 간의 내부 통신에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-242">These details are used for internal communication between the partner and Microsoft only.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f92ce-243">이메일 지원만 제공하려는 경우 **고객 지원** 섹션에서 더미 전화번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-243">If you want to provide only email support, enter a dummy phone number in the **Customer Support** section.</span></span> <span data-ttu-id="f92ce-244">이 경우에 사용자가 제공한 이메일을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-244">In this case, the email you provided is used instead.</span></span>
   >
   >
6. <span data-ttu-id="f92ce-245">**게시** 탭으로 이동하고 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-245">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="f92ce-246">스테이징 환경에서 제품을 테스트하는 방법에 대한 자세한 지침은 [Marketplace에서 VM 제품 테스트](marketplace-publishing-vm-image-test-in-staging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-246">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="f92ce-247">준비 단계에서 제품을 테스트한 후에 게시 포털에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-247">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-248">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-248">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![지원](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-the-categories"></a><span data-ttu-id="f92ce-250">범주 업데이트</span><span class="sxs-lookup"><span data-stu-id="f92ce-250">Update the categories</span></span>
<span data-ttu-id="f92ce-251">제품에 대한 범주 섹션을 업데이트하고 제품을 다시 게시하려면 다음과 같은 단계에 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-251">To update the categories section for your offer and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-252">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-252">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="f92ce-253">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-253">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-254">왼쪽 메뉴에서 **범주** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-254">In the menu on the left, click the **CATEGORIES** tab.</span></span>
4. <span data-ttu-id="f92ce-255">**범주** 섹션에서 제품에 대한 범주를 업데이트하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-255">In the **Categories** section, update the categories for your offer and save the changes.</span></span> <span data-ttu-id="f92ce-256">Azure Marketplace 갤러리에 대해 최대 5개의 범주를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-256">You can choose up to five categories for the Azure Marketplace gallery.</span></span>
5. <span data-ttu-id="f92ce-257">**게시** 탭으로 이동하고 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-257">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="f92ce-258">스테이징 환경에서 제품을 테스트하는 방법에 대한 자세한 지침은 [Marketplace에서 VM 제품 테스트](marketplace-publishing-vm-image-test-in-staging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-258">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
6. <span data-ttu-id="f92ce-259">준비 단계에서 제품을 테스트한 후에 게시 포털에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-259">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-260">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-260">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![범주](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a><span data-ttu-id="f92ce-262">나열된 제품에 새 SKU 추가</span><span class="sxs-lookup"><span data-stu-id="f92ce-262">Add a new SKU under a listed offer</span></span>
<span data-ttu-id="f92ce-263">라이브 제품에 새로운 SKU를 추가하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-263">To add a new SKU in your live offer, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-264">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-264">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="f92ce-265">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-265">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-266">왼쪽 메뉴에서 **SKU** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-266">In the menu on the left, click the **SKUS** tab.</span></span> <span data-ttu-id="f92ce-267">그런 다음 **SKU 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-267">Then click **Add a SKU**.</span></span> 
4. <span data-ttu-id="f92ce-268">대화 상자에서 **SKU 식별자**를 소문자로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-268">In the dialog box, enter a **SKU Identifier** in lowercase.</span></span> <span data-ttu-id="f92ce-269">BYOL 청구 모델로 새 SKU를 게시하려는 경우 **BYOL(사용자 라이선스 필요) 청구 모델** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-269">Select the **Bring your own license (BYOL) billing model** check box if you want to publish the new SKU with a BYOL billing model.</span></span> <span data-ttu-id="f92ce-270">그렇지 않으면 확인란의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-270">Otherwise, clear the check box.</span></span> <span data-ttu-id="f92ce-271">눈금 표시를 클릭하여 새로운 SKU를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-271">Click the tick mark to create a new SKU.</span></span> <span data-ttu-id="f92ce-272">BYOL 청구 모델을 선택하지 않은 경우 청구 모델은 매시간으로 자동 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-272">If you didn't choose the BYOL billing model, the billing model is automatically set to hourly.</span></span> <span data-ttu-id="f92ce-273">30일 체험 평가판을 매시간 요금 청구 모델로 사용하려면 **체험 평가판을 사용할 수 있나요?**에 **한 달**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-273">If you want the 30-day free trial for the hourly billing model, select **One Month** for **Is a free trial available?**</span></span> <span data-ttu-id="f92ce-274">그렇지 않은 경우 **평가판 없음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-274">Otherwise, select **No Trial**.</span></span> <span data-ttu-id="f92ce-275">(새로운 SKU를 만드는 동안 BYOL을 선택하지 않은 경우에만 **체험 평가판을 사용할 수 있나요?**가 나타납니다.)</span><span class="sxs-lookup"><span data-stu-id="f92ce-275">(**Is a free trial available?** appears only if you haven't selected BYOL while creating the new SKU.)</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f92ce-276">솔루션 템플릿을 게시하도록 승인한 경우*에만* **솔루션 템플릿을 통해 항상 구입되어야 하기 때문에 Marketplace에서 이 SKU를 숨깁니다**는 **예**로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-276">**Hide this SKU from the Marketplace because it should always be bought via a solution template** should be **Yes** *only* if you're approved for publishing a solution template.</span></span> <span data-ttu-id="f92ce-277">그렇지 않은 경우 이 옵션은 항상 **아니요**로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-277">Otherwise, this option should always be **No**.</span></span>
   >
   >
4. <span data-ttu-id="f92ce-278">왼쪽 메뉴에서 **VM 이미지** 탭을 클릭하고 사용자가 만든 새 SKU를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-278">In the menu on the left, click the **VM IMAGES** tab and find out the new SKU that you've created.</span></span>
5. <span data-ttu-id="f92ce-279">새로운 SKU를 설정하려면 지침으로 [VM 이미지에 대한 인증 가져오기](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-279">To set up the new SKU, see [Obtain certification for your VM image](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) for guidance.</span></span>
6. <span data-ttu-id="f92ce-280">새로운 SKU에 대한 마케팅 자료를 추가하려면 [Marketplace 마케팅 콘텐츠 제공](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-280">To add marketing material for the new SKU, see [Provide Marketplace marketing content](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>
7. <span data-ttu-id="f92ce-281">새로운 SKU에 대한 가격 책정 정보를 추가하려면 [가격 설정](marketplace-publishing-push-to-staging.md#step-2-set-your-prices)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-281">To add pricing information for the new SKU, see [Set your prices](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).</span></span>
8. <span data-ttu-id="f92ce-282">**게시** 탭으로 이동하고 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-282">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="f92ce-283">스테이징 환경에서 제품을 테스트하는 방법에 대한 자세한 지침은 [Marketplace에서 VM 제품 테스트](marketplace-publishing-vm-image-test-in-staging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-283">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
9. <span data-ttu-id="f92ce-284">준비 단계에서 제품을 테스트한 후에 게시 포털에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-284">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-285">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-285">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![SKU 추가](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-the-data-disk-count-for-a-listed-sku"></a><span data-ttu-id="f92ce-288">나열된 SKU에 대한 데이터 디스크 수 변경</span><span class="sxs-lookup"><span data-stu-id="f92ce-288">Change the data disk count for a listed SKU</span></span>
<span data-ttu-id="f92ce-289">나열된 SKU의 데이터 디스크 수를 늘리거나 줄일 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-289">You can't increment/decrement the data disk count of a listed SKU.</span></span> <span data-ttu-id="f92ce-290">이 경우 새로운 SKU를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-290">You need to create a new SKU in this case.</span></span> <span data-ttu-id="f92ce-291">자세한 지침은 [나열된 제품에 새 SKU 추가](#add-a-new-sku-under-a-listed-offer) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-291">For detailed guidance, refer to the section [Add a new SKU under a listed offer](#add-a-new-sku-under-a-listed-offer).</span></span>

## <a name="delete-a-listed-offer-from-the-marketplace"></a><span data-ttu-id="f92ce-292">Marketplace에서 나열된 제품 삭제</span><span class="sxs-lookup"><span data-stu-id="f92ce-292">Delete a listed offer from the Marketplace</span></span>
<span data-ttu-id="f92ce-293">라이브 제품을 제거하는 요청이 있는 경우에 다양한 측면을 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-293">Various aspects need to be taken care of in the case of a request to remove a live offer.</span></span> <span data-ttu-id="f92ce-294">Azure Marketplace에서 나열된 제품을 제거하기 위해 지원 팀의 지침을 가져오려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-294">To get guidance from the support team to remove a listed offer from the Marketplace, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-295">[인시던트 만들기](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) 페이지에서 지원 티켓을 발행합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-295">Raise a support ticket on the [Create an incident](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) page.</span></span>

2. <span data-ttu-id="f92ce-296">**제품 관리**로 **문제 형식**을 선택하고 **프로덕션 환경에서 제품 및/또는 SKU 수정**으로 **범주**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-296">Select **Problem type** as **Managing offers**, and select **Category** as **Modifying an offer and/or SKU already in production**.</span></span>
3. <span data-ttu-id="f92ce-297">요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-297">Submit the request.</span></span>

<span data-ttu-id="f92ce-298">지원 팀은 제품/SKU 삭제 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-298">The support team guides you through the offer/SKU deletion process.</span></span>

> [!NOTE]
> <span data-ttu-id="f92ce-299">[초안] 상태([스테이징] 또는 [프로덕션] 상태가 아님)인 동안에는 제품을 언제든지 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-299">You can always delete the offer while it is in Draft status (but not Staging or Production).</span></span> <span data-ttu-id="f92ce-300">**기록** 탭에서 **초안 버리기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-300">On the **HISTORY** tab, click **DISCARD DRAFT**.</span></span>
>
>

## <a name="delete-a-listed-sku-from-the-marketplace"></a><span data-ttu-id="f92ce-301">Marketplace에서 나열된 SKU 삭제</span><span class="sxs-lookup"><span data-stu-id="f92ce-301">Delete a listed SKU from the Marketplace</span></span>
<span data-ttu-id="f92ce-302">Marketplace에서 나열된 SKU를 삭제하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-302">To delete a listed SKU from the Marketplace, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-303">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-303">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="f92ce-304">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-304">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-305">왼쪽 창에서 **SKU** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-305">In the pane on the left, click the **SKUS** tab.</span></span>
4. <span data-ttu-id="f92ce-306">삭제할 SKU를 선택하고 **삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-306">Select the SKU that you want to delete, and click the **Delete** button.</span></span>
5. <span data-ttu-id="f92ce-307">[게시 포털]에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-307">Go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-308">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-308">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish the offer in the Marketplace.</span></span>
6. <span data-ttu-id="f92ce-309">Marketplace에 제품이 다시 게시되면 SKU가 Marketplace 및 Azure Portal에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-309">After the offer is republished in the Marketplace, the SKU is deleted from the Marketplace and the Azure portal.</span></span>

## <a name="delete-the-current-version-of-a-listed-sku-from-the-marketplace"></a><span data-ttu-id="f92ce-310">Marketplace에서 나열된 현재 버전의 SKU 삭제</span><span class="sxs-lookup"><span data-stu-id="f92ce-310">Delete the current version of a listed SKU from the Marketplace</span></span>
<span data-ttu-id="f92ce-311">Marketplace에서 나열된 현재 버전의 SKU를 삭제하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-311">To delete the current version of a listed SKU from the Marketplace, follow these steps:</span></span> 

1. <span data-ttu-id="f92ce-312">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-312">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="f92ce-313">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-313">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-314">왼쪽 메뉴에서 **VM 이미지** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-314">In the menu on the left, click the **VM IMAGES** tab.</span></span>
4. <span data-ttu-id="f92ce-315">현재 버전을 삭제할 SKU를 선택하고 **삭제** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-315">Select the SKU whose current version you want to delete, and click the **Delete** button.</span></span>
5. <span data-ttu-id="f92ce-316">[게시 포털]에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-316">Go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-317">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-317">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish the offer in the Marketplace.</span></span>
6. <span data-ttu-id="f92ce-318">Marketplace에 제품이 다시 게시되면 나열된 SKU의 현재 버전이 Marketplace 및 Azure Portal에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-318">After the offer gets republished in the Marketplace, the current version of the listed SKU is deleted from the Marketplace and the Azure portal.</span></span> <span data-ttu-id="f92ce-319">SKU는 이전 버전으로 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-319">The SKU is then rolled back to its previous version.</span></span>

## <a name="revert-the-listing-price-to-production-values"></a><span data-ttu-id="f92ce-320">나열 가격을 프로덕션 값으로 되돌리기</span><span class="sxs-lookup"><span data-stu-id="f92ce-320">Revert the listing price to production values</span></span>
<span data-ttu-id="f92ce-321">나열 가격을 프로덕션 값으로 되돌리려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-321">To revert the listing price to production values, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-322">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-322">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="f92ce-323">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-323">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-324">왼쪽 메뉴에서 **가격 책정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-324">In the menu on the left, click the **PRICING** tab.</span></span>
4. <span data-ttu-id="f92ce-325">가격 책정을 재설정할 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-325">Select a region whose pricing you want to reset.</span></span>

    ![가격 책정 지역](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. <span data-ttu-id="f92ce-327">시간당 청구 모델인 SKU의 경우 선택한 지역에 대한 프로덕션에 있으므로 모든 코어에 대한 가격을 재설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-327">For SKUs with an hourly billing model, reset the prices for all the cores as they are in production for the selected region.</span></span> <span data-ttu-id="f92ce-328">BYOL 청구 모델인 SKU의 경우 **외부 라이선스(BYOL) SKU 가용성Y** 섹션에서 SKU에 대한 확인란을 선택하여 해당 지역에서 SKU를 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-328">For SKUs with a BYOL billing model, make the SKU available in the region by selecting the check box for the SKU in the **EXTERNALLY-LICENSED (BYOL) SKU AVAILABILITY** section.</span></span>

    ![가격 책정 모델](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. <span data-ttu-id="f92ce-330">**미국의 가격에 따라 다른 마켓의 가격 자동 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-330">Click **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f92ce-331">버튼의 레이블은 선택한 지역에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-331">The button’s label might be different depending on the region that you select.</span></span> <span data-ttu-id="f92ce-332">미국을 선택했기 때문에 단추는 **미국의 가격에 따라 다른 마켓의 가격 자동 설정**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-332">Because we selected United States, the button is labeled **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES**.</span></span>
   >
   >

    ![가격 자동 설정](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. <span data-ttu-id="f92ce-334">[가격 자동 설정] 마법사의 1페이지에서 기본 시장을 선택하고 **화살표** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-334">On page 1 of the Autoprice wizard, choose the base market and click the **arrow** button.</span></span>

    ![기본 시장](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. <span data-ttu-id="f92ce-336">2페이지에서 서비스 계획 및 미터(코어)를 선택하고 **화살표** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-336">On page 2, choose service plans and meters (cores), and click the **arrow** button.</span></span>

    ![서비스 계획 및 미터](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. <span data-ttu-id="f92ce-338">3페이지에서 **모두 토글**을 클릭하여 모든 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-338">On page 3, click **Toggle All** to select all regions.</span></span> <span data-ttu-id="f92ce-339">또는 특정 지역에 대한 확인란을 수동으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-339">Or you can manually select check boxes for specific regions.</span></span> <span data-ttu-id="f92ce-340">**화살표** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-340">Click the **arrow** button.</span></span>

    ![시장 선택](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. <span data-ttu-id="f92ce-342">4페이지에서 환율을 검토하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-342">On page 4, review the exchange rates and click **Finish**.</span></span> <span data-ttu-id="f92ce-343">마법사는 선택 항목에 따라 가격 책정을 재설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-343">The wizard resets the pricing according to your selections.</span></span>

11. <span data-ttu-id="f92ce-344">**가격 책정** 탭에서 **변경 내용 및 요약 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-344">On the **PRICING** tab, click **VIEW SUMMARY AND CHANGES**.</span></span>
    <span data-ttu-id="f92ce-345">**버전 보기**에서 **초안**을 선택하고 **비교 대상**에서 **프로덕션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-345">For **View Version**, select **Draft**, and for **Compare with**, select **Production**.</span></span> <span data-ttu-id="f92ce-346">가격 책정에 차이점이 없으면 가격이 프로덕션 값으로 되돌려집니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-346">If you see no pricing difference, the pricing reverted to the production values successfully.</span></span>

    ![요약 및 변경 내용 보기](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. <span data-ttu-id="f92ce-348">**게시** 탭으로 이동하고 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-348">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="f92ce-349">스테이징 환경에서 제품을 테스트하는 방법에 대한 자세한 지침은 [Marketplace에서 VM 제품 테스트](marketplace-publishing-vm-image-test-in-staging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-349">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
13. <span data-ttu-id="f92ce-350">준비 단계에서 제품을 테스트한 후에 게시 포털에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-350">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-351">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-351">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

## <a name="revert-the-billing-model-to-production-values"></a><span data-ttu-id="f92ce-352">청구 모델을 프로덕션 값으로 되돌리기</span><span class="sxs-lookup"><span data-stu-id="f92ce-352">Revert the billing model to production values</span></span>
<span data-ttu-id="f92ce-353">청구 모델을 프로덕션 값으로 되돌리려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-353">To revert the billing model to production values, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-354">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-354">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="f92ce-355">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-355">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-356">왼쪽 메뉴에서 **SKU** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-356">In the menu on the left, click the **SKUS** tab.</span></span>
4. <span data-ttu-id="f92ce-357">**편집** 버튼을 클릭하여 요금 청구 모델을 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-357">Click the **Edit** button to revert the billing model.</span></span> <span data-ttu-id="f92ce-358">열린 창에서 **청구 및 라이선스를 Azure 외부에서 수행(사용자 라이선스 필요)** 확인란을 선택하거나 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-358">In the window that opens, select or clear the **Billing and licensing is done externally from Azure (aka Bring Your Own License)** check box.</span></span>

    ![청구 편집](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. <span data-ttu-id="f92ce-360">이 문서에서 "나열 가격을 프로덕션 값으로 되돌리기"의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-360">Follow the steps in "Revert the listing price to production values" in this article.</span></span>
6. <span data-ttu-id="f92ce-361">**게시** 탭으로 이동하고 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-361">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="f92ce-362">스테이징 환경에서 제품을 테스트하는 방법에 대한 자세한 지침은 [Marketplace에서 VM 제품 테스트](marketplace-publishing-vm-image-test-in-staging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-362">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="f92ce-363">준비 단계에서 제품을 테스트한 후에 게시 포털에서 **게시** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-363">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="f92ce-364">**프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-364">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

## <a name="revert-the-visibility-setting-of-a-listed-sku-to-the-production-value"></a><span data-ttu-id="f92ce-365">나열된 SKU의 표시 유형 설정을 프로덕션 값으로 되돌리기</span><span class="sxs-lookup"><span data-stu-id="f92ce-365">Revert the visibility setting of a listed SKU to the production value</span></span>
<span data-ttu-id="f92ce-366">나열된 SKU의 표시 유형 설정을 프로덕션 값으로 되돌리려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f92ce-366">To revert the visibility setting of a listed SKU to the production value, follow these steps:</span></span>

1. <span data-ttu-id="f92ce-367">[게시 포털](https://publish.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-367">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="f92ce-368">**가상 컴퓨터** 탭으로 이동하고 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-368">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="f92ce-369">왼쪽 메뉴에서 **SKU** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-369">In the menu on the left, click the **SKUS** tab.</span></span>
4. <span data-ttu-id="f92ce-370">SKU를 선택하고 SKU의 표시 여부 설정을 프로덕션 값으로 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-370">Select your SKU, and revert the visibility setting of the SKU to the production value.</span></span>

    ![표시 유형](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. <span data-ttu-id="f92ce-372">변경 내용을 수행한 후에 **프로덕션에 푸시하도록 요청 승인**을 클릭하여 Marketplace에서 제품을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f92ce-372">After you're done with the changes, click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

## <a name="see-also"></a><span data-ttu-id="f92ce-373">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f92ce-373">See also</span></span>
* [<span data-ttu-id="f92ce-374">시작: Azure Marketplace에 제품 게시</span><span class="sxs-lookup"><span data-stu-id="f92ce-374">Get Started: Publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="f92ce-375">지급 보고 이해</span><span class="sxs-lookup"><span data-stu-id="f92ce-375">Understand payout reporting</span></span>](marketplace-publishing-report-payout.md)
* [<span data-ttu-id="f92ce-376">클라우드 솔루션 공급자 재판매인 인센티브 변경</span><span class="sxs-lookup"><span data-stu-id="f92ce-376">Change your Cloud Solution Provider reseller incentive</span></span>](marketplace-publishing-csp-incentive.md)
* [<span data-ttu-id="f92ce-377">Marketplace에서 일반적인 게시 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f92ce-377">Troubleshoot common publishing problems in the Marketplace</span></span>](marketplace-publishing-support-common-issues.md)
* [<span data-ttu-id="f92ce-378">게시자로 지원 받기</span><span class="sxs-lookup"><span data-stu-id="f92ce-378">Get support as a publisher</span></span>](marketplace-publishing-get-publisher-support.md)
* [<span data-ttu-id="f92ce-379">온-프레미스 VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="f92ce-379">Create a VM image on-premises</span></span>](marketplace-publishing-vm-image-creation-on-premise.md)
* [<span data-ttu-id="f92ce-380">Azure Preview 포털에서 Windows를 실행하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="f92ce-380">Create a virtual machine running Windows in the Azure preview portal</span></span>](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

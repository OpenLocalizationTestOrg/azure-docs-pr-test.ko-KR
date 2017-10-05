---
title: "제품을 만들고 Marketplace에 배포하는 방법 개요 | Microsoft Docs"
description: "승인된 Microsoft 개발자가 되고, 가상 컴퓨터 이미지, 템플릿, 데이터 서비스 또는 개발자 서비스를 만들어서 Azure Marketplace에 배포하는 데 필요한 단계를 이해합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5343bd26-c6e4-4589-85b7-4a2c00bba8ab
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio
ms.openlocfilehash: 8fbf201343f6710d2781a4b56ae54833ed4c06cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-and-manage-an-offer-in-the-azure-marketplace"></a><span data-ttu-id="ca45f-103">Azure Marketplace에 제품 게시 및 관리</span><span class="sxs-lookup"><span data-stu-id="ca45f-103">Publish and manage an offer in the Azure Marketplace</span></span>
<span data-ttu-id="ca45f-104">다른 Azure 고객 및 파트너가 구매하여 사용하도록 개발자가 Azure Marketplace에 나열된 솔루션을 만들고, 배포하고, 관리하는 데 도움을 주기 위해 이 문서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-104">This article is provided to help developers create, deploy, and manage their solutions listed in the Azure Marketplace for other Azure customers and partners to purchase and use.</span></span>

## <a name="marketplace-publishing"></a><span data-ttu-id="ca45f-105">Marketplace 게시</span><span class="sxs-lookup"><span data-stu-id="ca45f-105">Marketplace publishing</span></span>
<span data-ttu-id="ca45f-106">Azure 게시자인 사용자는 Marketplace에서 다른 개발자, ISV 및 IT 전문가에게 혁신적인 솔루션 또는 서비스를 배포하고 판매할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-106">As an Azure publisher, you can distribute and sell your innovative solution or service to other developers, ISVs, and IT professionals in the Marketplace.</span></span> <span data-ttu-id="ca45f-107">Marketplace를 통해 클라우드 기반 응용 프로그램 및 모바일 솔루션을 신속하게 개발하려는 고객에게 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-107">Through the Marketplace, you can reach customers who want to quickly develop their cloud-based applications and mobile solutions.</span></span> <span data-ttu-id="ca45f-108">솔루션이 비즈니스 사용자를 대상으로 하는 경우 [AppSource](http://appsource.microsoft.com) Marketplace를 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-108">If your solution targets business users, you might want to consider the [AppSource](http://appsource.microsoft.com) marketplace.</span></span>


## <a name="supported-types-of-solutions"></a><span data-ttu-id="ca45f-109">지원되는 솔루션 형식</span><span class="sxs-lookup"><span data-stu-id="ca45f-109">Supported types of solutions</span></span>
<span data-ttu-id="ca45f-110">게시자로서 자신의 회사에서 제공할 솔루션의 종류를 정의하는 작업을 우선 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-110">The first thing you want to do as a publisher is to define what kind of solution your company is offering.</span></span> <span data-ttu-id="ca45f-111">Marketplace에서는 다음과 같은 종류의 제품을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-111">The Marketplace supports the following types of offers:</span></span>

|<span data-ttu-id="ca45f-112">솔루션 형식</span><span class="sxs-lookup"><span data-stu-id="ca45f-112">Solution type</span></span>|<span data-ttu-id="ca45f-113">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ca45f-113">Virtual machine</span></span>|<span data-ttu-id="ca45f-114">솔루션 템플릿</span><span class="sxs-lookup"><span data-stu-id="ca45f-114">Solution template</span></span>|
|---|---|---|
|<span data-ttu-id="ca45f-115">**정의**</span><span class="sxs-lookup"><span data-stu-id="ca45f-115">**Definition**</span></span>|<span data-ttu-id="ca45f-116">완전히 설치된 운영 체제 및 하나 이상의 응용 프로그램이 포함된 미리 구성된 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-116">Preconfigured images with a fully installed operating system and one or more applications.</span></span> <span data-ttu-id="ca45f-117">가상 컴퓨터 이미지는 Azure 가상 컴퓨터 서비스에서 가상 컴퓨터를 만들고 배포하는 데 필요한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-117">A virtual machine image provides the information necessary to create and deploy virtual machines in the Azure Virtual Machines service.</span></span>|<span data-ttu-id="ca45f-118">하나 이상의 서로 다른 Azure 서비스를 참조할 수 있는 데이터 구조는 다른 판매자가 게시한 서비스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-118">A data structure that can reference one or more distinct Azure services, including services published by other sellers.</span></span> <span data-ttu-id="ca45f-119">Azure 구독자는 단일 조정된 방식으로 하나 이상의 제품을 배포하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-119">Azure subscribers can use it to deploy one or more offerings in a single, coordinated manner.</span></span>|
|<span data-ttu-id="ca45f-120">**예제**</span><span class="sxs-lookup"><span data-stu-id="ca45f-120">**Example**</span></span>|<span data-ttu-id="ca45f-121">Azure 게시자인 사용자는 혁신적인 데이터베이스 서비스를 사용하여 VM을 만들고 유효성을 검사했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-121">As an Azure publisher, you've created and validated a VM with an innovative database service.</span></span> <span data-ttu-id="ca45f-122">다른 Azure 구독자는 해당 클라우드 서비스 환경에 이 VM을 확보하고 배포하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-122">Other Azure subscribers want to procure and deploy this VM into their cloud service environments.</span></span>|<span data-ttu-id="ca45f-123">Azure 게시자로 부하 분산, 강화된 보안 및 고가용성 기능을 갖춘 클라우드 서비스를 빠르게 배포할 수 있도록 하는 Azure의 서비스 집합을 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-123">As an Azure publisher, you've bundled a set of services from across Azure that make it quick to deploy cloud services with load balancing, enhanced security, and high availability.</span></span> <span data-ttu-id="ca45f-124">다른 Azure 구독자는 해당 목표를 충족하는 솔루션 템플릿을 확보하여 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-124">Other Azure subscribers can save time by procuring the solution template that meets their objective.</span></span> <span data-ttu-id="ca45f-125">동일하거나 유사한 Azure 서비스를 수동으로 찾고, 확보하고, 배포하고 구성하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-125">They don't have to manually locate, procure, deploy, and configure the same or similar Azure services.</span></span>|

> [!NOTE]
> <span data-ttu-id="ca45f-126">일부 단계는 여러 형식의 솔루션에서 공유되고 다른 단계는 각 솔루션 형식에 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-126">Some steps are shared between the different types of solutions, and others are distinct to the respective type of solution.</span></span> <span data-ttu-id="ca45f-127">이 문서에서는 모든 유형의 솔루션에 대해 완료해야 하는 단계에 대한 간략한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-127">This article provides a short overview of the steps you need to complete for any type of solution.</span></span>

## <a name="publish-a-solution"></a><span data-ttu-id="ca45f-128">솔루션 게시</span><span class="sxs-lookup"><span data-stu-id="ca45f-128">Publish a solution</span></span>
![추천, 등록, 게시](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a><span data-ttu-id="ca45f-130">사전 승인을 위한 솔루션 추천</span><span class="sxs-lookup"><span data-stu-id="ca45f-130">Nominate your solution for pre-approval</span></span>
<span data-ttu-id="ca45f-131">가상 컴퓨터 [솔루션](https://createopportunity.azurewebsites.net)을 Marketplace에 게시하려면 Microsoft Azure Certified **솔루션 추천 양식**을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-131">To publish a virtual machine [solution](https://createopportunity.azurewebsites.net) to the Marketplace, complete the Microsoft Azure Certified **Solution Nomination Form**.</span></span>

>[!NOTE]
> <span data-ttu-id="ca45f-132">파트너 계정 관리자나 DX 파트너 관리자와 함께 작업하는 경우에는 Azure Certified 프로그램에 솔루션을 추천해달라고 요청하세요.</span><span class="sxs-lookup"><span data-stu-id="ca45f-132">If you are working with a Partner Account Manager or a DX Partner Manager, ask them to nominate your solution for the Azure Certified program.</span></span> <span data-ttu-id="ca45f-133">또는 [Microsoft Azure Certified](http://createopportunity.azurewebsites.net) 웹 페이지로 이동하여 응용 프로그램 양식을 작성하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-133">You can also go to the [Microsoft Azure Certified](http://createopportunity.azurewebsites.net) webpage and fill out the application form.</span></span> <span data-ttu-id="ca45f-134">**Microsoft 스폰서 연락처** 상자에서 파트너 계정 관리자 또는 DX 파트너 관리자의 이메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-134">Enter the email of your Partner Account Manager or DX Partner Manager in the **Microsoft Sponsor Contact** box.</span></span>

<span data-ttu-id="ca45f-135">[Azure Marketplace 참여 정책](http://go.microsoft.com/fwlink/?LinkID=526833)의 자격 조건을 충족하고 응용 프로그램이 승인되면 Marketplace에 솔루션을 등록하기 위한 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-135">If you meet the eligibility criteria in the [Azure Marketplace participation policies](http://go.microsoft.com/fwlink/?LinkID=526833) and your application is approved, we start working with you to onboard your solution to the Marketplace.</span></span>

### <a name="register-your-account-as-a-microsoft-seller"></a><span data-ttu-id="ca45f-136">Microsoft 판매자로 계정 등록</span><span class="sxs-lookup"><span data-stu-id="ca45f-136">Register your account as a Microsoft seller</span></span>
<span data-ttu-id="ca45f-137">[Microsoft 개발자 계정](marketplace-publishing-accounts-creation-registration.md)으로 Microsoft 계정을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-137">Register your Microsoft account as a [Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md).</span></span>

### <a name="publish-your-solution"></a><span data-ttu-id="ca45f-138">솔루션 게시</span><span class="sxs-lookup"><span data-stu-id="ca45f-138">Publish your solution</span></span>
<span data-ttu-id="ca45f-139">솔루션을 Marketplace에 게시하려면 다음과 같은 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="ca45f-139">To publish a solution to the Marketplace, follow these steps:</span></span>
1. <span data-ttu-id="ca45f-140">비기술 요구 사항 충족</span><span class="sxs-lookup"><span data-stu-id="ca45f-140">Fulfill the nontechnical requirements.</span></span>

    <span data-ttu-id="ca45f-141">a.</span><span class="sxs-lookup"><span data-stu-id="ca45f-141">a.</span></span> <span data-ttu-id="ca45f-142">[비기술 필수 구성 요소](marketplace-publishing-pre-requisites.md) 충족</span><span class="sxs-lookup"><span data-stu-id="ca45f-142">Fulfill the [nontechnical prerequisites](marketplace-publishing-pre-requisites.md).</span></span>

    <span data-ttu-id="ca45f-143">b.</span><span class="sxs-lookup"><span data-stu-id="ca45f-143">b.</span></span> <span data-ttu-id="ca45f-144">[VM 기술 필수 구성 요소](marketplace-publishing-vm-image-creation-prerequisites.md) 충족</span><span class="sxs-lookup"><span data-stu-id="ca45f-144">Fulfill the [VM technical prerequisites](marketplace-publishing-vm-image-creation-prerequisites.md).</span></span>

    <span data-ttu-id="ca45f-145">c.</span><span class="sxs-lookup"><span data-stu-id="ca45f-145">c.</span></span> <span data-ttu-id="ca45f-146">[솔루션 템플릿 기술 필수 구성 요소](marketplace-publishing-solution-template-creation-prerequisites.md) 충족</span><span class="sxs-lookup"><span data-stu-id="ca45f-146">Fulfill the [solution template technical prerequisites](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span>

2. <span data-ttu-id="ca45f-147">제품 만들기</span><span class="sxs-lookup"><span data-stu-id="ca45f-147">Create your offer.</span></span>

    <span data-ttu-id="ca45f-148">a.</span><span class="sxs-lookup"><span data-stu-id="ca45f-148">a.</span></span> <span data-ttu-id="ca45f-149">[가상 컴퓨터](marketplace-publishing-vm-image-creation.md) 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="ca45f-149">Create a [virtual machine](marketplace-publishing-vm-image-creation.md) offer.</span></span>

    <span data-ttu-id="ca45f-150">b.</span><span class="sxs-lookup"><span data-stu-id="ca45f-150">b.</span></span> <span data-ttu-id="ca45f-151">[솔루션 템플릿](marketplace-publishing-solution-template-creation.md) 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="ca45f-151">Create a [solution template](marketplace-publishing-solution-template-creation.md) offer.</span></span>

3. <span data-ttu-id="ca45f-152">제품 [마케팅 콘텐츠](marketplace-publishing-push-to-staging.md) 만들기</span><span class="sxs-lookup"><span data-stu-id="ca45f-152">Create your offer [marketing content](marketplace-publishing-push-to-staging.md).</span></span>

4. <span data-ttu-id="ca45f-153">준비 단계에서 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="ca45f-153">Test your offer in staging.</span></span>

    <span data-ttu-id="ca45f-154">a.</span><span class="sxs-lookup"><span data-stu-id="ca45f-154">a.</span></span> <span data-ttu-id="ca45f-155">[준비 단계](marketplace-publishing-vm-image-test-in-staging.md)에서 VM 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="ca45f-155">Test your VM offer in [staging](marketplace-publishing-vm-image-test-in-staging.md).</span></span>

    <span data-ttu-id="ca45f-156">b.</span><span class="sxs-lookup"><span data-stu-id="ca45f-156">b.</span></span> <span data-ttu-id="ca45f-157">[준비 단계](marketplace-publishing-solution-template-test-in-staging.md)에서 솔루션 템플릿 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="ca45f-157">Test your solution template offer in [staging](marketplace-publishing-solution-template-test-in-staging.md).</span></span>

5. <span data-ttu-id="ca45f-158">[Marketplace](marketplace-publishing-push-to-production.md)로 제품 배포</span><span class="sxs-lookup"><span data-stu-id="ca45f-158">Deploy your offer to the [Marketplace](marketplace-publishing-push-to-production.md).</span></span>


### <a name="create-and-manage-a-virtual-machine-image"></a><span data-ttu-id="ca45f-159">가상 컴퓨터 이미지 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="ca45f-159">Create and manage a virtual machine image</span></span>
<span data-ttu-id="ca45f-160">다음과 같은 리소스를 사용하여 VM 이미지를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-160">Create and manage a VM image by using these resources:</span></span>
* <span data-ttu-id="ca45f-161">VM 이미지 [온-프레미스](marketplace-publishing-vm-image-creation-on-premise.md) 만들기</span><span class="sxs-lookup"><span data-stu-id="ca45f-161">Create a VM image [on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>
* <span data-ttu-id="ca45f-162">[Azure Portal에서 Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 실행하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="ca45f-162">Create a virtual machine running [Windows in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="ca45f-163">[Azure Portal에서 Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 실행하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="ca45f-163">Create a virtual machine running [Linux in the Azure portal](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="ca45f-164">[VHD를 만드는](marketplace-publishing-vm-image-creation-troubleshooting.md) 동안 발생하는 일반적인 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ca45f-164">Troubleshoot common issues encountered during [VHD creation](marketplace-publishing-vm-image-creation-troubleshooting.md).</span></span>

## <a name="manage-your-solution"></a><span data-ttu-id="ca45f-165">솔루션 관리</span><span class="sxs-lookup"><span data-stu-id="ca45f-165">Manage your solution</span></span>
<span data-ttu-id="ca45f-166">다음 리소스에서 도움말을 사용하여 솔루션을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="ca45f-166">Manage your solution with help from the following resources:</span></span>
* [<span data-ttu-id="ca45f-167">가상 컴퓨터 제품에 대한 사후 생성 가이드 참고</span><span class="sxs-lookup"><span data-stu-id="ca45f-167">Read the post-production guide for virtual machine offers</span></span>](marketplace-publishing-vm-image-post-publishing.md)
* [<span data-ttu-id="ca45f-168">제품 또는 SKU의 비기술적인 세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="ca45f-168">Update the nontechnical details of an offer or a SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [<span data-ttu-id="ca45f-169">제품 또는 SKU의 기술적인 세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="ca45f-169">Update the technical details of an offer or a SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [<span data-ttu-id="ca45f-170">나열된 제품에 새 SKU 추가</span><span class="sxs-lookup"><span data-stu-id="ca45f-170">Add a new SKU under a listed offer</span></span>](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [<span data-ttu-id="ca45f-171">나열된 SKU에 대한 데이터 디스크 수 변경</span><span class="sxs-lookup"><span data-stu-id="ca45f-171">Change the data disk count for a listed SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [<span data-ttu-id="ca45f-172">Marketplace에서 나열된 제품 삭제</span><span class="sxs-lookup"><span data-stu-id="ca45f-172">Delete a listed offer from the Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md)
* [<span data-ttu-id="ca45f-173">Marketplace에서 나열된 SKU 삭제</span><span class="sxs-lookup"><span data-stu-id="ca45f-173">Delete a listed SKU from the Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [<span data-ttu-id="ca45f-174">Marketplace에서 나열된 현재 버전의 SKU 삭제</span><span class="sxs-lookup"><span data-stu-id="ca45f-174">Delete the current version of a listed SKU from the Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [<span data-ttu-id="ca45f-175">나열 가격을 프로덕션 값으로 되돌리기</span><span class="sxs-lookup"><span data-stu-id="ca45f-175">Revert the listing price to production values</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [<span data-ttu-id="ca45f-176">청구 모델을 프로덕션 값으로 되돌리기</span><span class="sxs-lookup"><span data-stu-id="ca45f-176">Revert the billing model to production values</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [<span data-ttu-id="ca45f-177">나열된 SKU의 표시 유형 설정을 프로덕션 값으로 되돌리기</span><span class="sxs-lookup"><span data-stu-id="ca45f-177">Revert the visibility setting of a listed SKU to the production value</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [<span data-ttu-id="ca45f-178">클라우드 솔루션 공급자 재판매인 인센티브 변경</span><span class="sxs-lookup"><span data-stu-id="ca45f-178">Change your Cloud Solution Provider reseller incentive</span></span>](marketplace-publishing-csp-incentive.md)
* [<span data-ttu-id="ca45f-179">지급 보고 이해</span><span class="sxs-lookup"><span data-stu-id="ca45f-179">Understand your payout reporting</span></span>](marketplace-publishing-report-payout.md)
* [<span data-ttu-id="ca45f-180">게시자로 지원 받기</span><span class="sxs-lookup"><span data-stu-id="ca45f-180">Get support as a publisher</span></span>](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a><span data-ttu-id="ca45f-181">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ca45f-181">Additional resources</span></span>
[<span data-ttu-id="ca45f-182">Azure PowerShell 설정</span><span class="sxs-lookup"><span data-stu-id="ca45f-182">Set up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

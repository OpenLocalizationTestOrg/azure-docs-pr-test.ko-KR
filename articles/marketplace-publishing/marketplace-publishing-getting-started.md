---
title: "방법의 aaaOverview toocreate 및 제안을 toohello 마켓플레이스 배포 | Microsoft Docs"
description: "Hello 단계 필요한 toobecome는 승인 된 Microsoft developer를 이해 하 고 만들기 및 가상 컴퓨터 이미지, 템플릿, 데이터 서비스 또는 hello Azure Marketplace의에서 개발자 서비스를 배포 합니다."
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
ms.openlocfilehash: ac5480b98b8b1021a595db951ed9c974f74415dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-and-manage-an-offer-in-hello-azure-marketplace"></a><span data-ttu-id="1cf1b-103">게시 하 고 hello Azure Marketplace에서에서 제공 하는 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="1cf1b-103">Publish and manage an offer in hello Azure Marketplace</span></span>
<span data-ttu-id="1cf1b-104">이 문서는 toohelp 개발자가 만들고 배포 하 고 다른 Azure 고객 및 파트너 toopurchase 및 사용에 대 한 hello Azure Marketplace에에서 나열 된 자신의 솔루션 관리 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-104">This article is provided toohelp developers create, deploy, and manage their solutions listed in hello Azure Marketplace for other Azure customers and partners toopurchase and use.</span></span>

## <a name="marketplace-publishing"></a><span data-ttu-id="1cf1b-105">Marketplace 게시</span><span class="sxs-lookup"><span data-stu-id="1cf1b-105">Marketplace publishing</span></span>
<span data-ttu-id="1cf1b-106">게시자를 Azure로 배포 하 고 판매 혁신적인 솔루션 또는 Isv 서비스 tooother 개발자 및 IT 전문가 hello 마켓플레이스 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-106">As an Azure publisher, you can distribute and sell your innovative solution or service tooother developers, ISVs, and IT professionals in hello Marketplace.</span></span> <span data-ttu-id="1cf1b-107">Hello 마켓플레이스를 통해 도달할 수 있습니다 tooquickly 하려는 고객의 클라우드 기반 응용 프로그램 및 모바일 솔루션을 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-107">Through hello Marketplace, you can reach customers who want tooquickly develop their cloud-based applications and mobile solutions.</span></span> <span data-ttu-id="1cf1b-108">솔루션에서 비즈니스 사용자를 대상으로 하는 경우 tooconsider hello 할 수 있습니다 [AppSource](http://appsource.microsoft.com) 마켓플레이스입니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-108">If your solution targets business users, you might want tooconsider hello [AppSource](http://appsource.microsoft.com) marketplace.</span></span>


## <a name="supported-types-of-solutions"></a><span data-ttu-id="1cf1b-109">지원되는 솔루션 형식</span><span class="sxs-lookup"><span data-stu-id="1cf1b-109">Supported types of solutions</span></span>
<span data-ttu-id="1cf1b-110">hello 먼저 게시자 toodefine 어떤 종류의 솔루션 회사 제공 하는 대로 toodo 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-110">hello first thing you want toodo as a publisher is toodefine what kind of solution your company is offering.</span></span> <span data-ttu-id="1cf1b-111">마켓플레이스 hello hello 제안 유형만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-111">hello Marketplace supports hello following types of offers:</span></span>

|<span data-ttu-id="1cf1b-112">솔루션 형식</span><span class="sxs-lookup"><span data-stu-id="1cf1b-112">Solution type</span></span>|<span data-ttu-id="1cf1b-113">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="1cf1b-113">Virtual machine</span></span>|<span data-ttu-id="1cf1b-114">솔루션 템플릿</span><span class="sxs-lookup"><span data-stu-id="1cf1b-114">Solution template</span></span>|
|---|---|---|
|<span data-ttu-id="1cf1b-115">**정의**</span><span class="sxs-lookup"><span data-stu-id="1cf1b-115">**Definition**</span></span>|<span data-ttu-id="1cf1b-116">완전히 설치된 운영 체제 및 하나 이상의 응용 프로그램이 포함된 미리 구성된 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-116">Preconfigured images with a fully installed operating system and one or more applications.</span></span> <span data-ttu-id="1cf1b-117">가상 컴퓨터 이미지 정보 필요한 toocreate hello를 제공 하 고 hello Azure 가상 컴퓨터 서비스에서에서 가상 컴퓨터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-117">A virtual machine image provides hello information necessary toocreate and deploy virtual machines in hello Azure Virtual Machines service.</span></span>|<span data-ttu-id="1cf1b-118">하나 이상의 서로 다른 Azure 서비스를 참조할 수 있는 데이터 구조는 다른 판매자가 게시한 서비스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-118">A data structure that can reference one or more distinct Azure services, including services published by other sellers.</span></span> <span data-ttu-id="1cf1b-119">Azure 구독자가 toodeploy 사용할 수 있는 단일 조정 된 방식으로 하나 이상의 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-119">Azure subscribers can use it toodeploy one or more offerings in a single, coordinated manner.</span></span>|
|<span data-ttu-id="1cf1b-120">**예제**</span><span class="sxs-lookup"><span data-stu-id="1cf1b-120">**Example**</span></span>|<span data-ttu-id="1cf1b-121">Azure 게시자인 사용자는 혁신적인 데이터베이스 서비스를 사용하여 VM을 만들고 유효성을 검사했습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-121">As an Azure publisher, you've created and validated a VM with an innovative database service.</span></span> <span data-ttu-id="1cf1b-122">다른 Azure 구독자 tooprocure 원하고이 VM의 클라우드 서비스 환경에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-122">Other Azure subscribers want tooprocure and deploy this VM into their cloud service environments.</span></span>|<span data-ttu-id="1cf1b-123">게시자를 Azure로 부하 분산, 향상 된 보안 및 고가용성을 사용 하 여 빠른 toodeploy 클라우드 서비스를 구성 하는 Azure 전체에서 서비스의 집합을 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-123">As an Azure publisher, you've bundled a set of services from across Azure that make it quick toodeploy cloud services with load balancing, enhanced security, and high availability.</span></span> <span data-ttu-id="1cf1b-124">다른 Azure 구독자의 목표를 충족 하는 hello 솔루션 템플릿을 확보 하 여 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-124">Other Azure subscribers can save time by procuring hello solution template that meets their objective.</span></span> <span data-ttu-id="1cf1b-125">찾을, 받기, 배포 및 구성 toomanually 있지 않아도 hello 동일 하거나 유사한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-125">They don't have toomanually locate, procure, deploy, and configure hello same or similar Azure services.</span></span>|

> [!NOTE]
> <span data-ttu-id="1cf1b-126">몇 가지 단계가 hello 다른 유형의 솔루션을 간에 공유 되 고, 나머지는 솔루션의 고유한 toohello 각각의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-126">Some steps are shared between hello different types of solutions, and others are distinct toohello respective type of solution.</span></span> <span data-ttu-id="1cf1b-127">이 여기서는 간단한 개요를 제공 hello 단계의 모든 유형의 솔루션에 대 한 toocomplete 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-127">This article provides a short overview of hello steps you need toocomplete for any type of solution.</span></span>

## <a name="publish-a-solution"></a><span data-ttu-id="1cf1b-128">솔루션 게시</span><span class="sxs-lookup"><span data-stu-id="1cf1b-128">Publish a solution</span></span>
![추천, 등록, 게시](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a><span data-ttu-id="1cf1b-130">사전 승인을 위한 솔루션 추천</span><span class="sxs-lookup"><span data-stu-id="1cf1b-130">Nominate your solution for pre-approval</span></span>
<span data-ttu-id="1cf1b-131">toopublish 가상 컴퓨터 [솔루션](https://createopportunity.azurewebsites.net) toohello 마켓플레이스를 Microsoft Azure 인증 완료 hello **솔루션 추천 양식을**합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-131">toopublish a virtual machine [solution](https://createopportunity.azurewebsites.net) toohello Marketplace, complete hello Microsoft Azure Certified **Solution Nomination Form**.</span></span>

>[!NOTE]
> <span data-ttu-id="1cf1b-132">파트너 계정 관리자 또는 DX 파트너 관리자와 작업 하는 경우 달라고 toonominate hello Azure 인증 프로그램에 대 한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-132">If you are working with a Partner Account Manager or a DX Partner Manager, ask them toonominate your solution for hello Azure Certified program.</span></span> <span data-ttu-id="1cf1b-133">Toohello 넘어가면 [Microsoft Azure 인증](http://createopportunity.azurewebsites.net) 웹 페이지 및 사용자에 게 응용 프로그램 폼 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-133">You can also go toohello [Microsoft Azure Certified](http://createopportunity.azurewebsites.net) webpage and fill out hello application form.</span></span> <span data-ttu-id="1cf1b-134">Hello에 파트너 계정 관리자 또는 DX 파트너 관리자의 전자 메일 hello 입력 **Microsoft 스폰서 연락처** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-134">Enter hello email of your Partner Account Manager or DX Partner Manager in hello **Microsoft Sponsor Contact** box.</span></span>

<span data-ttu-id="1cf1b-135">Hello에 hello 자격 조건을 충족 하는 경우 [Azure 마켓플레이스 참여 정책](http://go.microsoft.com/fwlink/?LinkID=526833) 및 응용 프로그램 승인 되 면 있습니다 tooonboard 사용자 솔루션 toohello 마켓플레이스 사용을 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-135">If you meet hello eligibility criteria in hello [Azure Marketplace participation policies](http://go.microsoft.com/fwlink/?LinkID=526833) and your application is approved, we start working with you tooonboard your solution toohello Marketplace.</span></span>

### <a name="register-your-account-as-a-microsoft-seller"></a><span data-ttu-id="1cf1b-136">Microsoft 판매자로 계정 등록</span><span class="sxs-lookup"><span data-stu-id="1cf1b-136">Register your account as a Microsoft seller</span></span>
<span data-ttu-id="1cf1b-137">[Microsoft 개발자 계정](marketplace-publishing-accounts-creation-registration.md)으로 Microsoft 계정을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-137">Register your Microsoft account as a [Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md).</span></span>

### <a name="publish-your-solution"></a><span data-ttu-id="1cf1b-138">솔루션 게시</span><span class="sxs-lookup"><span data-stu-id="1cf1b-138">Publish your solution</span></span>
<span data-ttu-id="1cf1b-139">toopublish 솔루션 toohello 마켓플레이스를 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-139">toopublish a solution toohello Marketplace, follow these steps:</span></span>
1. <span data-ttu-id="1cf1b-140">Hello 일반 요구 사항을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-140">Fulfill hello nontechnical requirements.</span></span>

    <span data-ttu-id="1cf1b-141">a.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-141">a.</span></span> <span data-ttu-id="1cf1b-142">Hello 충족 [배경이 필수 구성 요소](marketplace-publishing-pre-requisites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-142">Fulfill hello [nontechnical prerequisites](marketplace-publishing-pre-requisites.md).</span></span>

    <span data-ttu-id="1cf1b-143">b.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-143">b.</span></span> <span data-ttu-id="1cf1b-144">Hello 충족 [VM 기술 필수 구성 요소](marketplace-publishing-vm-image-creation-prerequisites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-144">Fulfill hello [VM technical prerequisites](marketplace-publishing-vm-image-creation-prerequisites.md).</span></span>

    <span data-ttu-id="1cf1b-145">c.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-145">c.</span></span> <span data-ttu-id="1cf1b-146">Hello 충족 [솔루션 템플릿 필수 구성 요소 기술](marketplace-publishing-solution-template-creation-prerequisites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-146">Fulfill hello [solution template technical prerequisites](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span>

2. <span data-ttu-id="1cf1b-147">제품 만들기</span><span class="sxs-lookup"><span data-stu-id="1cf1b-147">Create your offer.</span></span>

    <span data-ttu-id="1cf1b-148">a.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-148">a.</span></span> <span data-ttu-id="1cf1b-149">[가상 컴퓨터](marketplace-publishing-vm-image-creation.md) 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="1cf1b-149">Create a [virtual machine](marketplace-publishing-vm-image-creation.md) offer.</span></span>

    <span data-ttu-id="1cf1b-150">b.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-150">b.</span></span> <span data-ttu-id="1cf1b-151">[솔루션 템플릿](marketplace-publishing-solution-template-creation.md) 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="1cf1b-151">Create a [solution template](marketplace-publishing-solution-template-creation.md) offer.</span></span>

3. <span data-ttu-id="1cf1b-152">제품 [마케팅 콘텐츠](marketplace-publishing-push-to-staging.md) 만들기</span><span class="sxs-lookup"><span data-stu-id="1cf1b-152">Create your offer [marketing content](marketplace-publishing-push-to-staging.md).</span></span>

4. <span data-ttu-id="1cf1b-153">준비 단계에서 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="1cf1b-153">Test your offer in staging.</span></span>

    <span data-ttu-id="1cf1b-154">a.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-154">a.</span></span> <span data-ttu-id="1cf1b-155">[준비 단계](marketplace-publishing-vm-image-test-in-staging.md)에서 VM 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="1cf1b-155">Test your VM offer in [staging](marketplace-publishing-vm-image-test-in-staging.md).</span></span>

    <span data-ttu-id="1cf1b-156">b.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-156">b.</span></span> <span data-ttu-id="1cf1b-157">[준비 단계](marketplace-publishing-solution-template-test-in-staging.md)에서 솔루션 템플릿 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="1cf1b-157">Test your solution template offer in [staging](marketplace-publishing-solution-template-test-in-staging.md).</span></span>

5. <span data-ttu-id="1cf1b-158">제안 toohello 배포 [마켓플레이스](marketplace-publishing-push-to-production.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-158">Deploy your offer toohello [Marketplace](marketplace-publishing-push-to-production.md).</span></span>


### <a name="create-and-manage-a-virtual-machine-image"></a><span data-ttu-id="1cf1b-159">가상 컴퓨터 이미지 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="1cf1b-159">Create and manage a virtual machine image</span></span>
<span data-ttu-id="1cf1b-160">다음과 같은 리소스를 사용하여 VM 이미지를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-160">Create and manage a VM image by using these resources:</span></span>
* <span data-ttu-id="1cf1b-161">VM 이미지 [온-프레미스](marketplace-publishing-vm-image-creation-on-premise.md) 만들기</span><span class="sxs-lookup"><span data-stu-id="1cf1b-161">Create a VM image [on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>
* <span data-ttu-id="1cf1b-162">실행 중인 가상 컴퓨터 만들기 [Windows hello Azure 포털에서에서](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-162">Create a virtual machine running [Windows in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="1cf1b-163">실행 중인 가상 컴퓨터 만들기 [hello Azure 포털에서에서 Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-163">Create a virtual machine running [Linux in hello Azure portal](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="1cf1b-164">[VHD를 만드는](marketplace-publishing-vm-image-creation-troubleshooting.md) 동안 발생하는 일반적인 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1cf1b-164">Troubleshoot common issues encountered during [VHD creation](marketplace-publishing-vm-image-creation-troubleshooting.md).</span></span>

## <a name="manage-your-solution"></a><span data-ttu-id="1cf1b-165">솔루션 관리</span><span class="sxs-lookup"><span data-stu-id="1cf1b-165">Manage your solution</span></span>
<span data-ttu-id="1cf1b-166">Hello 다음 리소스에서에서 사용 하 여 솔루션을 관리:</span><span class="sxs-lookup"><span data-stu-id="1cf1b-166">Manage your solution with help from hello following resources:</span></span>
* [<span data-ttu-id="1cf1b-167">가상 컴퓨터에 대 한 읽기 hello 제작 후 가이드는</span><span class="sxs-lookup"><span data-stu-id="1cf1b-167">Read hello post-production guide for virtual machine offers</span></span>](marketplace-publishing-vm-image-post-publishing.md)
* [<span data-ttu-id="1cf1b-168">제공 하는 서비스 또는 SKU의 hello 기술 세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="1cf1b-168">Update hello nontechnical details of an offer or a SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [<span data-ttu-id="1cf1b-169">제공 하는 서비스 또는 SKU의 hello 기술 세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="1cf1b-169">Update hello technical details of an offer or a SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [<span data-ttu-id="1cf1b-170">나열된 제품에 새 SKU 추가</span><span class="sxs-lookup"><span data-stu-id="1cf1b-170">Add a new SKU under a listed offer</span></span>](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [<span data-ttu-id="1cf1b-171">나열 된 SKU에 대 한 hello 데이터 디스크 개수 변경</span><span class="sxs-lookup"><span data-stu-id="1cf1b-171">Change hello data disk count for a listed SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [<span data-ttu-id="1cf1b-172">Hello Marketplace에서에서 나열 된 제안을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-172">Delete a listed offer from hello Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md)
* [<span data-ttu-id="1cf1b-173">Hello Marketplace에서에서 나열 된 SKU를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-173">Delete a listed SKU from hello Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [<span data-ttu-id="1cf1b-174">Hello Marketplace에서에서 나열 된 SKU의 hello 현재 버전을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cf1b-174">Delete hello current version of a listed SKU from hello Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [<span data-ttu-id="1cf1b-175">가격 tooproduction 값을 나열 하는 hello 되돌리기</span><span class="sxs-lookup"><span data-stu-id="1cf1b-175">Revert hello listing price tooproduction values</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [<span data-ttu-id="1cf1b-176">청구 모델 tooproduction 값 hello 되돌리기</span><span class="sxs-lookup"><span data-stu-id="1cf1b-176">Revert hello billing model tooproduction values</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [<span data-ttu-id="1cf1b-177">나열 된 SKU toohello 프로덕션 값의 표시 유형 설정 hello 되돌리기</span><span class="sxs-lookup"><span data-stu-id="1cf1b-177">Revert hello visibility setting of a listed SKU toohello production value</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [<span data-ttu-id="1cf1b-178">클라우드 솔루션 공급자 재판매인 인센티브 변경</span><span class="sxs-lookup"><span data-stu-id="1cf1b-178">Change your Cloud Solution Provider reseller incentive</span></span>](marketplace-publishing-csp-incentive.md)
* [<span data-ttu-id="1cf1b-179">지급 보고 이해</span><span class="sxs-lookup"><span data-stu-id="1cf1b-179">Understand your payout reporting</span></span>](marketplace-publishing-report-payout.md)
* [<span data-ttu-id="1cf1b-180">게시자로 지원 받기</span><span class="sxs-lookup"><span data-stu-id="1cf1b-180">Get support as a publisher</span></span>](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a><span data-ttu-id="1cf1b-181">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1cf1b-181">Additional resources</span></span>
[<span data-ttu-id="1cf1b-182">Azure PowerShell 설정</span><span class="sxs-lookup"><span data-stu-id="1cf1b-182">Set up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

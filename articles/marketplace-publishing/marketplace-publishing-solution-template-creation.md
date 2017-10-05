---
title: "Marketplace용 솔루션 템플릿 만들기 가이드 | Microsoft Docs"
description: "Azure 마켓플레이스에서 구입하기 위한 여러 VM 이미지 솔루션 템플릿을 만들고 인증하고 배포하는 방법에 대한 자세한 지침입니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b753bfb4bd69bd9aacf4eebd8999397394c28bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="9e38e-103">Azure 마켓플레이스용 솔루션 템플릿 만들기 가이드</span><span class="sxs-lookup"><span data-stu-id="9e38e-103">Guide to create a solution template for Azure Marketplace</span></span>
<span data-ttu-id="9e38e-104">1단계 [계정 만들기 및 등록][link-acct-creation]을 완료한 후 [솔루션 템플릿을 만들기 위한 기술 필수 조건](marketplace-publishing-solution-template-creation-prerequisites.md)에서 Azure 호환 솔루션 템플릿 만들기에 대해 안내했습니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on the creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="9e38e-105">이제 Azure Marketplace의 [게시 포털][link-pubportal]에서 여러 VM에 대한 솔루션 템플릿을 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-105">Now we will walk you through the steps for creating a solution template for multiple VMs on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-the-publishing-portal"></a><span data-ttu-id="9e38e-106">게시 포털에서 솔루션 템플릿 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="9e38e-106">Create your solution template offer in the Publishing Portal</span></span>
<span data-ttu-id="9e38e-107">[https://publish.windowsazure.com](http://publish.windowsazure.com)로 이동합니다. 처음으로 [게시 포털](https://publish.windowsazure.com/)에 로그인할 때는 회사의 판매자 프로필이 등록된 계정을 동일하게 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9e38e-107">Go to  [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for the first time to the [Publishing Portal](https://publish.windowsazure.com/), use the same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="9e38e-108">나중에 게시 포털에서 회사의 직원을 공동 관리자로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-108">Later, you can add any employee of your company as a co-admin in the Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="9e38e-109">1. "솔루션 템플릿" 선택</span><span class="sxs-lookup"><span data-stu-id="9e38e-109">1. Select "Solution templates"</span></span>
  ![drawing][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="9e38e-111">2. 새 솔루션 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="9e38e-111">2. Create a new solution template</span></span>
  ![drawing][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="9e38e-113">3. 토폴로지로 시작</span><span class="sxs-lookup"><span data-stu-id="9e38e-113">3. Start with topologies</span></span>
<span data-ttu-id="9e38e-114">솔루션 템플릿은 해당하는 모든 토폴로지의 "부모"입니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-114">A solution template is a "parent" to all of its topologies.</span></span> <span data-ttu-id="9e38e-115">하나의 제품/솔루션 템플릿에서 여러 토폴로지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="9e38e-116">제품이 스테이징으로 푸시될 때 해당 토폴로지도 모두 함께 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-116">When an offer is pushed to staging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="9e38e-117">아래 단계를 따라 제품을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-117">Follow the steps below to define your offer:</span></span>     

* <span data-ttu-id="9e38e-118">토폴로지 만들기: "토폴로지 식별자"는 일반적으로 솔루션 템플릿의 토폴로지 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-118">Create a Topology: “Topology Identifier” is typically the name of the topology for the solution template.</span></span> <span data-ttu-id="9e38e-119">토폴로지 식별자는 아래와 같은 URL에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-119">The topology identifier is used in the URL as shown below:</span></span>

  <span data-ttu-id="9e38e-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="9e38e-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="9e38e-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="9e38e-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="9e38e-122">새 버전을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="9e38e-123">4. 토폴로지 버전 인증받기</span><span class="sxs-lookup"><span data-stu-id="9e38e-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="9e38e-124">해당하는 특정 토폴로지 버전을 프로비전하는 데 필요한 모든 파일이 포함된 zip 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-124">Upload a zip file that contains all required files to provision that particular version of the topology.</span></span> <span data-ttu-id="9e38e-125">이 zip 파일에는 다음이 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-125">This zip file must contain the following:</span></span>

* <span data-ttu-id="9e38e-126">루트 디렉터리의 *mainTemplate.json* 및 *createUiDefinition.json* 파일</span><span class="sxs-lookup"><span data-stu-id="9e38e-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="9e38e-127">연결된 모든 템플릿 및 모든 필수 스크립트</span><span class="sxs-lookup"><span data-stu-id="9e38e-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="9e38e-128">개발자가 솔루션 템플릿 토폴로지를 만들고 인증을 받는 동안 회사의 비즈니스, 마케팅 및/또는 법무 부서는 마케팅 및 법률 콘텐츠를 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-128">While your developers work on creating the solution template topologies and getting them certified, the business, marketing, and/or legal departments of your company can work on the marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="9e38e-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9e38e-129">Next steps</span></span>
<span data-ttu-id="9e38e-130">지금까지 솔루션 템플릿을 만들고 zip 파일을 업로드했으므로 제품을 스테이징으로 푸시하기 전에 [마켓플레이스 마케팅 콘텐츠 가이드](marketplace-publishing-push-to-staging.md) 의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="9e38e-130">Now that you created your solution template and uploaded the zip file, please follow the instructions in the [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing the offer to staging.</span></span> <span data-ttu-id="9e38e-131">[시작: Azure 마켓플레이스에 제품을 게시하는 방법](marketplace-publishing-getting-started.md)을 참조하여 전체 마켓플레이스 게시 문서를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-131">To see the full set of marketplace publishing articles, visit [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="9e38e-132">다음 관련 문서를 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e38e-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="9e38e-133">VM 이미지: [Azure의 가상 컴퓨터 이미지 정보](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="9e38e-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="9e38e-134">VM 확장: [VM 에이전트 및 VM 확장 개요](https://msdn.microsoft.com/library/azure/dn832621.aspx) 및 [Azure VM 확장 및 기능](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="9e38e-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="9e38e-135">Azure Resource Manager: [Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md) 및 [간단한 템플릿 예제](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="9e38e-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="9e38e-136">저장소 계정 제한: [저장소 계정 제한을 모니터링하는 방법](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) 및 [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="9e38e-136">Storage account throttles: [How to Monitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com

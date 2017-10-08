---
title: "aaaGuide toocreating hello 마켓플레이스를 위한 솔루션 템플릿 | Microsoft Docs"
description: "Toocreate, 인증 및 hello Azure Marketplace에서 구입에 대 한 다중 VM 이미지 솔루션 템플릿을 배포 방법을 설명 합니다."
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
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="ffb5e-103">Azure 마켓플레이스 toocreate 솔루션 템플릿을 안내합니다</span><span class="sxs-lookup"><span data-stu-id="ffb5e-103">Guide toocreate a solution template for Azure Marketplace</span></span>
<span data-ttu-id="ffb5e-104">1 단계를 완료 한 후 [계정 만들기 및 등록][link-acct-creation], 우리 있습니다 hello 만들기에 Azure 호환 솔루션 서식 파일의 단계별 [을 만들기 위한 필수 구성 요소를 기술는 솔루션 템플릿을](marketplace-publishing-solution-template-creation-prerequisites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on hello creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="ffb5e-105">이제 우리는 단계를 안내 hello 여러 Vm hello에 대 한 솔루션 템플릿을 만들기 위한 [게시 포털] [ link-pubportal] hello Azure Marketplace에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-105">Now we will walk you through hello steps for creating a solution template for multiple VMs on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a><span data-ttu-id="ffb5e-106">Hello 게시 포털에에서 사용자 솔루션 템플릿을 제안을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-106">Create your solution template offer in hello Publishing Portal</span></span>
<span data-ttu-id="ffb5e-107">너무 이동 [https://publish.windowsazure.com](http://publish.windowsazure.com)합니다. 첫 번째 시간 toohello hello에 대 한 로그인 할 때 [게시 포털](https://publish.windowsazure.com/)를 사용 하 여 hello 회사의 판매자 프로필 등록 된 계정과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-107">Go too [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for hello first time toohello [Publishing Portal](https://publish.windowsazure.com/), use hello same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="ffb5e-108">이상에서는 hello 게시 포털에서에서 공동 관리자로 모든 직원이 회사의를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-108">Later, you can add any employee of your company as a co-admin in hello Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="ffb5e-109">1. "솔루션 템플릿" 선택</span><span class="sxs-lookup"><span data-stu-id="ffb5e-109">1. Select "Solution templates"</span></span>
  ![drawing][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="ffb5e-111">2. 새 솔루션 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="ffb5e-111">2. Create a new solution template</span></span>
  ![drawing][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="ffb5e-113">3. 토폴로지로 시작</span><span class="sxs-lookup"><span data-stu-id="ffb5e-113">3. Start with topologies</span></span>
<span data-ttu-id="ffb5e-114">솔루션 템플릿은 해당 토폴로지의 "부모" tooall입니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-114">A solution template is a "parent" tooall of its topologies.</span></span> <span data-ttu-id="ffb5e-115">하나의 제품/솔루션 템플릿에서 여러 토폴로지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="ffb5e-116">제안을 toostaging 푸시를 모든 해당 토폴로지에 하 여 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-116">When an offer is pushed toostaging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="ffb5e-117">제안을 toodefine 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-117">Follow hello steps below toodefine your offer:</span></span>     

* <span data-ttu-id="ffb5e-118">토폴로지 생성: 일반적으로 "토폴로지 식별자" hello 솔루션 템플릿에 대 한 hello 토폴로지의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-118">Create a Topology: “Topology Identifier” is typically hello name of hello topology for hello solution template.</span></span> <span data-ttu-id="ffb5e-119">아래와 같이 hello 토폴로지 식별자 hello URL에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-119">hello topology identifier is used in hello URL as shown below:</span></span>

  <span data-ttu-id="ffb5e-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="ffb5e-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="ffb5e-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="ffb5e-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="ffb5e-122">새 버전을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="ffb5e-123">4. 토폴로지 버전 인증받기</span><span class="sxs-lookup"><span data-stu-id="ffb5e-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="ffb5e-124">모든 필수 파일 tooprovision hello 토폴로지의 특정 버전을 포함 하는 zip 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-124">Upload a zip file that contains all required files tooprovision that particular version of hello topology.</span></span> <span data-ttu-id="ffb5e-125">이 zip 파일 hello 다음을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-125">This zip file must contain hello following:</span></span>

* <span data-ttu-id="ffb5e-126">루트 디렉터리의 *mainTemplate.json* 및 *createUiDefinition.json* 파일</span><span class="sxs-lookup"><span data-stu-id="ffb5e-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="ffb5e-127">연결된 모든 템플릿 및 모든 필수 스크립트</span><span class="sxs-lookup"><span data-stu-id="ffb5e-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="ffb5e-128">프로그램 개발자가 hello 솔루션 템플릿을 토폴로지를 만들고 얻거나 인증 hello 비즈니스에 작업 하는 동안, 마케팅 및/또는 법률 부서에 hello 마케팅 및 법적 콘텐츠 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-128">While your developers work on creating hello solution template topologies and getting them certified, hello business, marketing, and/or legal departments of your company can work on hello marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="ffb5e-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ffb5e-129">Next steps</span></span>
<span data-ttu-id="ffb5e-130">솔루션 템플릿을 생성 하 고 hello zip 파일을 업로드 하세요 hello 지침에에서 따라 hello [마켓플레이스 마케팅 콘텐츠 가이드](marketplace-publishing-push-to-staging.md) hello 제공 toostaging 푸시하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-130">Now that you created your solution template and uploaded hello zip file, please follow hello instructions in hello [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing hello offer toostaging.</span></span> <span data-ttu-id="ffb5e-131">toosee hello 전체 집합 문서를 게시 하는 marketplace의 참조 [시작: 어떻게 제공 toohello Azure 마켓플레이스 toopublish](marketplace-publishing-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-131">toosee hello full set of marketplace publishing articles, visit [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="ffb5e-132">다음 관련 문서를 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffb5e-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="ffb5e-133">VM 이미지: [Azure의 가상 컴퓨터 이미지 정보](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="ffb5e-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="ffb5e-134">VM 확장: [VM 에이전트 및 VM 확장 개요](https://msdn.microsoft.com/library/azure/dn832621.aspx) 및 [Azure VM 확장 및 기능](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="ffb5e-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="ffb5e-135">Azure Resource Manager: [Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md) 및 [간단한 템플릿 예제](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="ffb5e-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="ffb5e-136">저장소 계정 제한: [어떻게 저장소 계정 제한에 대 한 tooMonitor](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) 및 [프리미엄 저장소](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="ffb5e-136">Storage account throttles: [How tooMonitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com

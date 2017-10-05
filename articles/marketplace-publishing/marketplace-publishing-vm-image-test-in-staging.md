---
title: "Marketplace용 VM 제품 테스트 | Microsoft Docs"
description: "Azure 마켓플레이스용 VM 이미지를 테스트하는 방법을 이해합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: 26f856059b381be91b9cdd1f98a11dc90813c0c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-vm-offer-for-the-azure-marketplace-in-staging"></a><span data-ttu-id="f77bc-103">스테이징에서 Azure 마켓플레이스용 VM 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="f77bc-103">Test your VM offer for the Azure Marketplace in staging</span></span>
<span data-ttu-id="f77bc-104">스테이징이란 SKU를 마켓플레이스에 배포하기 전에 기능을 테스트하고 확인할 수 있는 사설 "샌드박스"에 배포하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it to the Marketplace.</span></span> <span data-ttu-id="f77bc-105">그러면 SKU는 배포한 고객에게 표시되는 것처럼 스테이징으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-105">The SKU appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="f77bc-106">VM 이미지는 인증되어야만 스테이징으로 푸시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-106">Your VM image must be certified to be pushed to staging.</span></span>

## <a name="step-1-push-your-offer-to-staging"></a><span data-ttu-id="f77bc-107">1단계: 제품을 스테이징으로 푸시</span><span class="sxs-lookup"><span data-stu-id="f77bc-107">Step 1: Push your offer to staging</span></span>
1. <span data-ttu-id="f77bc-108">**게시** 탭에서 **스테이징으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-108">On the **Publish** tab, click **Push to Staging**.</span></span>
   
    ![drawing](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="f77bc-110">게시 포털에서 오류에 대한 알림이 표시되는 경우 오류를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-110">If the Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="f77bc-111">**스테이징된 제품에 액세스할 수 있는 사람** 대화 상자에서 [Azure Preview 포털](https://portal.azure.com)에서 제품을 미리 보는 데 사용할 Azure 구독 목록을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-111">In the **Who can access your staged offer?** dialog box, enter the list of Azure subscriptions that you will use to preview your offer in the [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f77bc-112">가상 컴퓨터 및 솔루션 템플릿의 경우 CSP, DreamSpark 또는 Azure in Open 형식의 구독을 허용 목록에 **추가하지 마세요** .</span><span class="sxs-lookup"><span data-stu-id="f77bc-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="f77bc-113">가상 컴퓨터의 경우 **스테이징으로 푸시**버튼을 클릭하면 백그라운드에서 다음 단계가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-113">In case of Virtual Machines, when you click on the button **PUSH TO STAGING**, the following steps are performed behind the scene.</span></span> <span data-ttu-id="f77bc-114">게시 포털의 게시 탭에서 각 단계의 진행 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span></span> <span data-ttu-id="f77bc-115">이 페이지에서 목표에 따라 수정이 필요한 오류 정보가 있는지를 정기적으로 확인해야 합니다(상태가 "스테이징됨"으로 표시될 때까지).</span><span class="sxs-lookup"><span data-stu-id="f77bc-115">You must check this page at regular interval (until the status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="f77bc-116">처음에 스테이징 요청이 VHD의 유효성을 검사하는 인증 팀으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-116">At first your staging request goes to the certification team who validate the vhd.</span></span> <span data-ttu-id="f77bc-117">그러나 요청에 마케팅 변경만 포함되는 경우 인증 단계가 건너뛰어 집니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-117">However, if your request has got only marketing change, then the certification step is skipped.</span></span>
    > - <span data-ttu-id="f77bc-118">인증이 완료되면 제품의 복제가 모든 Azure 데이터 센터에서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-118">Once the certification is complete, replication of the offer start across all the Azure datacenters.</span></span> <span data-ttu-id="f77bc-119">일반적으로 복제가 완료되는 데는 24~48시간이 걸리지만 VHD의 크기에 따라 1주일까지 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-119">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span></span> <span data-ttu-id="f77bc-120">그러나 요청에 마케팅 변경만 포함되는 경우 복제가 더 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-120">However, if your request has got only marketing change, then the replication is faster.</span></span>
    > - <span data-ttu-id="f77bc-121">복제가 완료되면 [Azure 포털](http:/portal.azure.com)에서 제품을 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-121">When the replication is complete, then the offer will be available in the [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="f77bc-122">이때 상태는 게시 포털에서 "스테이징됨"이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-122">At that time the status become STAGED in the Publishing portal.</span></span> <span data-ttu-id="f77bc-123">스테이징된 제품은 제품이 스테이징되는 구독과 연결된 전자 메일 ID를 사용할 때만 [Azure 포털](http:/portal.azure.com) 에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-123">A staged offer is visible in the [Azure portal](http:/portal.azure.com) only using the email id(s) associated with the subscription with which the offer is staged.</span></span>

1. <span data-ttu-id="f77bc-124">이전 단계에서 나열된 Azure 구독 중 하나를 사용하여 [Azure Preview 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-124">Sign in to the [Azure preview portal](https://portal.azure.com) by using one of the Azure subscriptions listed in the previous step.</span></span>
2. <span data-ttu-id="f77bc-125">제품을 찾고 VM 이미지 지점의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="f77bc-126">마케팅 콘텐츠가 마켓플레이스에 올바르게 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-126">Make sure that marketing content shows up correctly in the Marketplace.</span></span>
   * <span data-ttu-id="f77bc-127">VM 이미지의 종단 간 배포</span><span class="sxs-lookup"><span data-stu-id="f77bc-127">End-to-end deployment of the VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="f77bc-129">제품을 프로덕션으로 푸시할 준비가 되었다고 게시 포털을 통해 Microsoft에 알릴 때까지[**게시** 탭 > **"프로덕션으로 푸시 승인 요청"** 버튼 클릭] 제품은 스테이징으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-129">Your offer will remain in staging until you notify Microsoft via the Publishing Portal [**Publish** tab > click on the button **"Request Approval to Push to Production"**] that you are ready to push to production.</span></span> <span data-ttu-id="f77bc-130">이 시간 동안 팀의 모든 구성원이 제품을 나열할 준비가 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-130">This is an ideal time to have all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="f77bc-131">스테이징 플랫폼은 게시자가 미리 보기 모드에서 제품을 테스트할 수 있도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-131">The staging platform is designed for testing the offer in a preview mode by the publisher.</span></span> <span data-ttu-id="f77bc-132">이 플랫폼은 상용으로는 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f77bc-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f77bc-133">Next steps</span></span>
<span data-ttu-id="f77bc-134">제품이 "스테이징"되었고 제품의 기능 및 마케팅 콘텐츠를 테스트했으므로 최종 게시 단계인 **4단계**, [마켓플레이스에 제품 배포](marketplace-publishing-push-to-production.md)를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f77bc-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed to the final publishing phase, **Step 4**: [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f77bc-135">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f77bc-135">See also</span></span>
* [<span data-ttu-id="f77bc-136">시작: Azure 마켓플레이스에 제품을 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="f77bc-136">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)


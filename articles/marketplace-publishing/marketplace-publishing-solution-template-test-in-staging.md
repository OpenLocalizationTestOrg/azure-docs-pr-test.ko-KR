---
title: "Marketplace용 솔루션 템플릿 제품 테스트 | Microsoft Docs"
description: "Azure 마켓플레이스에 대한 솔루션 템플릿 제품을 테스트하는 방법을 이해합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: ef8f9b5e-b98c-49f3-913f-cdf772c14c12
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/04/2015
ms.author: hascipio; v-divte
ms.openlocfilehash: da1fc4713fd1d832c7ba91226f72cbef63b241bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="9f92e-103">준비 단계에서 솔루션 템플릿 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="9f92e-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="9f92e-104">준비 단계에서는 제품을 프로덕션에 게시하기 전에 개인 "샌드박스"에 배포하여 기능을 테스트 및 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="9f92e-105">그러면 제안은 배포한 고객에게 표시되는 것처럼 스테이징으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-105">The offer appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="9f92e-106">제품이 준비 단계에 푸시되려면 인증되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-106">Your offer must be certified to be pushed to staging.</span></span>

<span data-ttu-id="9f92e-107">제품이 준비되면 [Azure 포털](https://portal.azure.com/)에서 제품을 보고 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-107">After the offer is staged, you can view and test the offer in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="9f92e-108">제품을 준비 단계에 푸시하고 [Azure 포털](https://portal.azure.com/)에서 테스트하려면 아래 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="9f92e-108">Follow the steps below to push your offer to staging and test it in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="9f92e-109">[포털 게시](https://publish.windowsazure.com) > **솔루션 템플릿** 탭 -> 제품 -> **게시** > **준비 단계로 푸시**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-109">Go to the [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push to Staging**.</span></span>
2. <span data-ttu-id="9f92e-110">제품 미리 보기 및 테스트를 위해 사용할 Azure 구독 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-110">Provide the list of Azure subscriptions that you will use to preview and test your offer.</span></span>
3. <span data-ttu-id="9f92e-111">이전 단계에서 사용한 구독 ID를 사용하여 Azure Preview 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-111">Sign in to the Azure preview portal by using the subscription ID that you used in the previous step.</span></span>
4. <span data-ttu-id="9f92e-112">아래 언급된 지점에 있는 Azure Preview 포털에서 테스트를 한 번 이상 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-112">Carry out at least one round of testing in the Azure preview portal on the points mentioned below:</span></span>
   * <span data-ttu-id="9f92e-113">마케팅 콘텐츠가 Azure 마켓플레이스에 올바르게 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-113">Make sure that marketing content shows up correctly in the Azure Marketplace.</span></span>
   * <span data-ttu-id="9f92e-114">토폴로지의 종단간 배포</span><span class="sxs-lookup"><span data-stu-id="9f92e-114">End-to-end deployment of the topology.</span></span>
   * <span data-ttu-id="9f92e-115">성능 테스트 및 스트레스 테스트 수행</span><span class="sxs-lookup"><span data-stu-id="9f92e-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="9f92e-116">토폴로지가 모범 사례에 부합하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-116">Ensure that your topology adheres to the best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f92e-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f92e-117">Next steps</span></span>
<span data-ttu-id="9f92e-118">결과에 만족하면 최종 제품 게시 단계인 **4단계**: [마켓플레이스에 제품 배포](marketplace-publishing-push-to-production.md)로 진행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-118">If you are satisfied with the results, then you can proceed to the final offer publishing phase, **Step 4**:  [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="9f92e-119">그렇지 않은 경우 제품을 변경하고 다시 인증 요청을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="9f92e-120">마케팅 콘텐츠를 변경한 경우에는 인증이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f92e-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="9f92e-121">모든 게시자 작업에 대한 지침은 [시작: Azure 마켓플레이스를 제공하는 서비스를 게시하는 방법](marketplace-publishing-getting-started.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f92e-121">See [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md) for a guide to all publisher tasks.</span></span>


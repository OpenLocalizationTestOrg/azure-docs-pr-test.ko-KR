---
title: "마켓플레이스 hello에 대 한 솔루션 템플릿을 제공 aaaTesting | Microsoft Docs"
description: "어떻게 tootest 솔루션 템플릿을 시 제공 hello Azure 마켓플레이스를 이해 합니다."
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
ms.openlocfilehash: 9c195c465d2fc6aa349e4bbcc348e5325f32850d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="e7460-103">준비 단계에서 솔루션 템플릿 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="e7460-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="e7460-104">개인 테스트 하 고 tooproduction 푸시하기 전에 해당 기능을 확인 수 "샌드박스"에 있는 제품을 배포 하는 수단을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="e7460-105">hello 제공이 배포 tooa 고객과 마찬가지로 준비에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-105">hello offer appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="e7460-106">제안을 푸시 인증 된 toobe toostaging 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-106">Your offer must be certified toobe pushed toostaging.</span></span>

<span data-ttu-id="e7460-107">보고 하 고 테스트할 수 hello 행사를 준비 하는 후 hello에서 hello 제공 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-107">After hello offer is staged, you can view and test hello offer in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="e7460-108">제안 toostaging toopush 아래 hello 단계를 수행 하 고 hello 테스트할 [Azure 포털](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="e7460-108">Follow hello steps below toopush your offer toostaging and test it in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="e7460-109">Toohello 이동 [게시 포털](https://publish.windowsazure.com) > **솔루션 템플릿을** 탭 > 제안을 > **게시** > **tooStaging 푸시** .</span><span class="sxs-lookup"><span data-stu-id="e7460-109">Go toohello [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push tooStaging**.</span></span>
2. <span data-ttu-id="e7460-110">Toopreview를 사용 하 고 제안을 테스트 됩니다는 hello Azure 구독 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-110">Provide hello list of Azure subscriptions that you will use toopreview and test your offer.</span></span>
3. <span data-ttu-id="e7460-111">Hello 이전 단계에서 사용 하는 hello 구독 ID를 사용 하 여 toohello Azure preview 포털에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-111">Sign in toohello Azure preview portal by using hello subscription ID that you used in hello previous step.</span></span>
4. <span data-ttu-id="e7460-112">아래에 언급 된 hello 지점에서 hello Azure 미리 보기 포털에서 하나 이상의 테스트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-112">Carry out at least one round of testing in hello Azure preview portal on hello points mentioned below:</span></span>
   * <span data-ttu-id="e7460-113">콘텐츠를 마케팅에 표시 되는지 올바르게 hello Azure 마켓플레이스 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-113">Make sure that marketing content shows up correctly in hello Azure Marketplace.</span></span>
   * <span data-ttu-id="e7460-114">Hello 토폴로지의 종단 간 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-114">End-to-end deployment of hello topology.</span></span>
   * <span data-ttu-id="e7460-115">성능 테스트 및 스트레스 테스트 수행</span><span class="sxs-lookup"><span data-stu-id="e7460-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="e7460-116">토폴로지에 toohello 모범 사례에 부합 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-116">Ensure that your topology adheres toohello best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7460-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e7460-117">Next steps</span></span>
<span data-ttu-id="e7460-118">Hello 결과 만족 하는 경우 다음 단계에서 게시 toohello 최종 제품을 계속 진행할 수 있습니다 **4 단계**: [배포 하 여 제안을 toohello 마켓플레이스](marketplace-publishing-push-to-production.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-118">If you are satisfied with hello results, then you can proceed toohello final offer publishing phase, **Step 4**:  [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="e7460-119">그렇지 않은 경우 제품을 변경하고 다시 인증 요청을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="e7460-120">마케팅 콘텐츠를 변경한 경우에는 인증이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="e7460-121">참조 [시작: 어떻게 제공 toohello Azure 마켓플레이스 toopublish](marketplace-publishing-getting-started.md) 가이드 tooall 게시자 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7460-121">See [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md) for a guide tooall publisher tasks.</span></span>


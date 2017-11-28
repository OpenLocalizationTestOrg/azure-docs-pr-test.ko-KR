---
title: "aaaGuide toocreating 마켓플레이스 hello에 대 한 데이터 서비스 | Microsoft Docs"
description: "Toocreate, 인증 하 고에 대 한 데이터 서비스를 배포 하는 방법의 자세한 지침은 hello Azure Marketplace에서 구입 합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a><span data-ttu-id="d25c3-103">Azure 마켓플레이스 hello에 대 한 데이터 서비스 게시 가이드</span><span class="sxs-lookup"><span data-stu-id="d25c3-103">Data Service Publishing Guide for hello Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d25c3-104">**현재는 새 데이터 서비스 게시자 등록을 더 이상 받지 않고 있습니다. 따라서 새 데이터 서비스 등재 승인을 받을 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="d25c3-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="d25c3-105">SaaS 비즈니스 응용 프로그램의 경우 원하는 toopublish AppSource에 자세한 정보를 찾을 수 [여기](https://appsource.microsoft.com/partners)합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="d25c3-106">IaaS 응용 프로그램 또는 서비스 개발자 경우는 Azure 마켓플레이스에서 toopublish 같은 자세한 정보를 찾을 수 [여기](https://azure.microsoft.com/marketplace/programs/certified/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="d25c3-107">Hello 1 단계를 완료 한 후 [계정 만들기 및 등록](marketplace-publishing-accounts-creation-registration.md), 우리를 안내 하 hello [일반 기술 이외의 기타](marketplace-publishing-pre-requisites.md) 및 [기술 요구 사항](marketplace-publishing-data-service-creation-prerequisites.md) 의 데이터 서비스 Azure 마켓플레이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-107">After completing hello step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through hello [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="d25c3-108">이제 우리는 단계를 안내 hello hello에 데이터 서비스 제공을 만드는 데 [게시 포털] [ link-pubportal] hello Azure Marketplace에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-108">Now we will walk you through hello steps for creating a Data Service offer on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="1----login-toohello-publishing-portal"></a><span data-ttu-id="d25c3-109">1.    로그인 toohello 게시 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-109">1.    Login toohello Publishing Portal.</span></span>
<span data-ttu-id="d25c3-110">너무 이동[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="d25c3-110">Go too[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="d25c3-111">**첫 번째 시간 로그인 tooPublishing 포털, 회사의 판매자에 프로 파일링 된 동일한 계정 개발자 센터에 등록 되었습니다. hello를 사용 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d25c3-111">**For first time login tooPublishing Portal, use hello same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="d25c3-112">(나중에 추가할 수 있습니다 모든 직원이 회사의 hello 게시 포털에서에서 공동 관리자로).</span><span class="sxs-lookup"><span data-stu-id="d25c3-112">(Later you can add any employee of your company as a co-admin in hello Publishing Portal).</span></span>

<span data-ttu-id="d25c3-113">Hello 클릭 **데이터 서비스를 게시** 이 hello hello 게시 포털에 처음 로그인 하는 경우 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-113">Click on hello **Publish a Data Services** tile if this is hello first login into hello publishing portal.</span></span>

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a><span data-ttu-id="d25c3-114">2.    선택 **데이터 서비스** hello hello 왼쪽 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-114">2.    Choose **Data Services** in hello navigation menu on hello left side.</span></span>
  ![drawing](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="d25c3-116">3.    새 데이터 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="d25c3-117">에 새 데이터 서비스 제공에 대 한 hello 제목에 채운 hello 오른쪽에 "+"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-117">Fill in hello title for your new Data Service Offer and click on “+” on hello right.</span></span>

  ![drawing](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a><span data-ttu-id="d25c3-119">4.    Hello 아래에서 검토 hello 하위 메뉴에서 새로 만든 데이터 서비스의 hello 탐색 메뉴.</span><span class="sxs-lookup"><span data-stu-id="d25c3-119">4.    Review hello sub-menu under hello newly created Data Service in hello navigation menu.</span></span>
<span data-ttu-id="d25c3-120">Hello 클릭 **연습** 탭 하 고 필요한 하 toopublish hello Azure Marketplace에서 데이터 서비스 제대로 hello에 필요한 모든 단계를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-120">Click on hello **Walkthrough** tab and review all necessary steps needed toopublish properly hello Data Service on hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="d25c3-121">항상 hello "연습" 페이지의 hello 링크를 클릭 하거나 hello 왼쪽에 hello 데이터 서비스 제품의 하위 메뉴에 탭을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-121">You always can click on hello links in hello “Walkthrough” page or use tabs on hello Data Service offer’s sub-menu on hello left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="d25c3-122">5.    새 플랜을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="d25c3-123">제품, 플랜, 트랜잭션.</span><span class="sxs-lookup"><span data-stu-id="d25c3-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="d25c3-124">각 제품에 플랜이 여러 개 있어도 되는데, 적어도 플랜이 하나(1) 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="d25c3-125">최종 사용자가 구독 tooyour 제공 hello 행사 계획 중 하나에 대 한 구독.</span><span class="sxs-lookup"><span data-stu-id="d25c3-125">When end-users subscribe tooyour offer they subscribe for one of hello offer’s Plan.</span></span> <span data-ttu-id="d25c3-126">각 계획은 최종 사용자는 어떻게 정의 수 toouse 서비스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-126">Each plan defines how end-users will be able toouse your service.</span></span>

<span data-ttu-id="d25c3-127">현재 Azure 마켓플레이스 데이터 서비스에 대 한 월간 구독 트랜잭션 기반 모델만 지원, 즉, 최종 사용자에 게 tooand를 구독 하는 hello 특정 계획의 toohello 가격에 따라 월별 요금 지불의 각 월 수 수 tooconsume 됩니다 hello 계획에 정의 된 트랜잭션입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according toohello price of hello specific plan they subscribed tooand will be able tooconsume each month number of transaction defined by hello plan.</span></span>

<span data-ttu-id="d25c3-128">일반적으로 데이터 서비스는를 반환 하는 레코드의 수로 정의 된 각 트랜잭션에 쿼리를 기반으로 hello toohello 서비스를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-128">Each Transaction usually defined as number of records your Data Service will return based on hello query sent toohello Service.</span></span> <span data-ttu-id="d25c3-129">hello 기본값은 100입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-129">hello default is 100.</span></span> <span data-ttu-id="d25c3-130">트랜잭션 수가 tooeach 쿼리 됩니다. 반환 된 레코드 수가 100로 나뉘고 toohello 가장 가까운 정수로 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-130">Number of transactions returned tooeach query will be number of records divided by 100 and rounded up toohello closest integer.</span></span>

<span data-ttu-id="d25c3-131">각 쿼리에 사용 되는 트랜잭션의 Azure 마켓플레이스 서비스 계층 책임 toomonitor (미터) 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-131">It’s Azure Marketplace Service layer responsibility toomonitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d25c3-132">Hello 달간 hello 트랜잭션 제한에 도달 하는 최종 사용자가을 toouse hello 서비스의 월간 구독 주기가 끝날 때까지 계속할 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-132">End-Users which reached hello transaction limit during hello month will be blocked from continuing toouse hello service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="d25c3-133">hello 계획 또는 hello 계획 중 하나 (하지만 해야 하지) 트랜잭션 무제한으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-133">hello plan or one of hello plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="d25c3-134">플랜을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-134">Create a plan.</span></span>
1. <span data-ttu-id="d25c3-135">클릭 **"+"** 다음 toohello "새 계획 추가"입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-135">Click on **“+”** next toohello “Add a new plan”.</span></span>
2. <span data-ttu-id="d25c3-136">Hello 옵션 중 하나 선택: **무제한** 또는 **제한** 이 계획에 대 한 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-136">Choose one of hello options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="d25c3-137">제한 한 다음 트랜잭션 hello 계획 hello 수를 제공 하는 경우 한 달에 tooconsume를 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-137">If Limited then provide hello number of transaction hello plan will allow tooconsume in a month.</span></span>
   
    ![drawing](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="d25c3-139">게시 포털에서는 또한 제안 "계획 식별자" 사용된 toocommunicate toohello 최종 사용자 UI hello에 hello 계획의 이름을 hello와 hello 마켓플레이스 서비스 tooidentify hello 계획 에서도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-139">Publishing Portal will also suggest “Plan Identifier”, which will be used toocommunicate toohello end-users hello name of hello plan in hello UI and also used by hello Market Place Service tooidentify hello Plan.</span></span> <span data-ttu-id="d25c3-140">원하는 경우 hello "계획 식별자"를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-140">You can change hello “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d25c3-141">"계획 식별자" hello 각 제안의 hello 범위 내에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-141">hello “Plan Identifier” must be unique within hello scope of each offer.</span></span> <span data-ttu-id="d25c3-142">다른 많은 식별자에서 사용 되는 hello 식별자가 잠겨 지 hello 첫 번째 게시 tooproduction 하 고 됩니다 수 toochange 후 게시 포털 계획이 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-142">As many other Identifiers used in hello Publishing Portal Plan identifier will be locked after hello first publishing tooproduction and you will not be able toochange this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="d25c3-143">Tooaccept 원하는 옵션을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-143">Click tooaccept your choice.</span></span>
4. <span data-ttu-id="d25c3-144">새로 만든 플랜에 대한 몇 가지 추가 질문을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![그리기](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="d25c3-146">질문</span><span class="sxs-lookup"><span data-stu-id="d25c3-146">Question</span></span> | <span data-ttu-id="d25c3-147">중요도</span><span class="sxs-lookup"><span data-stu-id="d25c3-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="d25c3-148">**이 계획은 무료이며 전 세계에서 사용할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="d25c3-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="d25c3-149">완전 무료 플랜을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="d25c3-150">hello –이 제품에만 계획을 게시 하는 "무료 제공" hello Marketplace에서에서 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-150">If it’s hello only plan for this offer – it means that you are publishing “Free Offer” in hello Marketplace.</span></span> <span data-ttu-id="d25c3-151">지원 되는 몇) (중 하나에이 계획을 hello는 옵션 toooffer 최종 사용자에 게 toolearn 상대적으로 적은 수의 월별 트랜잭션 수를 사용 하 여 서비스에 대 한 자세한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-151">If it’s only for one (of few) Plan, hello it gives you an option toooffer end-users toolearn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="d25c3-152">Hello 응답은 "Yes"를 추가 질문이 없습니다 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-152">If hello answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="d25c3-153">최종 사용자가 계획 유료 toohello를 업그레이드할 항상 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-153">End users can always upgrade toohello paid plans.</span></span>
> 
> 

| <span data-ttu-id="d25c3-154">질문</span><span class="sxs-lookup"><span data-stu-id="d25c3-154">Question</span></span> | <span data-ttu-id="d25c3-155">중요도</span><span class="sxs-lookup"><span data-stu-id="d25c3-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="d25c3-156">**무료 평가판이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="d25c3-156">**Is free trial available?**</span></span> |<span data-ttu-id="d25c3-157">전혀 "평가판 아니요" 중에서 선택할 수도 있고 옵션 toouse "ׁ ´ "에 대 한 계획을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-157">You can choose between “No Trial” at all or give an option toouse your Plan for “One Month”.</span></span> <span data-ttu-id="d25c3-158">게시자에는이 옵션 tooprovide 최종 사용자에 게 hello 가능성 toounderstand hello의 hello 얻을 이점 무료를 1 개월 동안 toouse를 같은입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-158">Publishers like toouse this option tooprovide end-users hello possibility toounderstand hello benefits of hello offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d25c3-159">최종 사용자에 게는 결제 수단과 신용 카드, 예: 기업 계약 설정 된 경우에 수 toopurchase 무료 평가판 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-159">End-users will only be able toopurchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="d25c3-160">Hello 무료 평가판의 1 개월 후 Azure 마켓플레이스 시작 됩니다 hello 가격 hello 구독의 hello 날짜를 기준으로 고객 충전 hello 고객 hello 구독 취소 초기화 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="d25c3-160">After one month of hello free trial, Azure Marketplace will start charging customers hello price as of hello date of hello subscription, unless hello customer initiated hello subscription cancellation.</span></span> <span data-ttu-id="d25c3-161">특별 한 알림 없음 toohello 최종 사용자에 게 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-161">No special notification will be provided toohello end-users.</span></span>
> 
> 

| <span data-ttu-id="d25c3-162">질문</span><span class="sxs-lookup"><span data-stu-id="d25c3-162">Question</span></span> | <span data-ttu-id="d25c3-163">중요도</span><span class="sxs-lookup"><span data-stu-id="d25c3-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="d25c3-164">**이 계획에는 프로 모션 코드 toopurchase를 필요로 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d25c3-164">**This plan requires a promotion code toopurchase?**</span></span> |<span data-ttu-id="d25c3-165">게시자 "A Promocode" toospecific 고객 라는 특수 한 코드를 제공 하 여 서비스를 계획 하는 옵션 toolimit 액세스 tootheir가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-165">Publishers have an option toolimit access tootheir Service Plans by providing a special code, called “A Promocode” toospecific customers.</span></span> <span data-ttu-id="d25c3-166">이 Promocode를 포함 하는 최종 사용자만 수 toosubscribe toohello 계획 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-166">Only end-users which will have this Promocode will be able toosubscribe toohello Plan.</span></span> <span data-ttu-id="d25c3-167">"No" 인 선택한 경우 hello를 제공 하는 hello 영역에서 모든 사용자가 사용할 수 있는 동의 (참조 [마켓플레이스 마케팅 콘텐츠 가이드](marketplace-publishing-push-to-staging.md) 자세한 내용을 보려면) 수 toosubscribe toothis 계획 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-167">If you choose “No”, then you agree that everyone from hello region where hello offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able toosubscribe toothis plan.</span></span> <span data-ttu-id="d25c3-168">더 이상 질문이 나오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="d25c3-169">**유효한 프로모션 코드가 없는 사용자에게도 이 플랜을 숨길까요?**</span><span class="sxs-lookup"><span data-stu-id="d25c3-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="d25c3-170">Hello 응답 toohello 이전 질문은 "Yes" 하는 경우 게시자 hello를 hello hello Marketplace의 UI에에서 표시이 계획을 제거 하는 옵션 toocompletely에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-170">If hello answer toohello previous question is “Yes” hello Publisher has an option toocompletely remove this plan from appearing in hello UI of hello Marketplace.</span></span> <span data-ttu-id="d25c3-171">그러나 고객 hello 제품 세부 정보 페이지에서이 계획을 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-171">It means, customers will not see this plan in hello Offer’s details page.</span></span> <span data-ttu-id="d25c3-172">Promocode toopurchase를 수신할 최종 사용자가는 것이 promocode를 사용 하 여 수 toosubscribe tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-172">End-users which will receive a promocode toopurchase it, will be able toosubscribe tooit using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="d25c3-173">6.    마켓플레이스 마케팅 콘텐츠를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="d25c3-174">Tooprovide 정보에 필요 하는 방법에 대 한 **마케팅, 가격, 지원 및 범주** 탭을 방문 하십시오 [마켓플레이스 마케팅 콘텐츠 가이드](marketplace-publishing-push-to-staging.md) hello에 게시 된 공통 tooall 아티팩트는 Azure 마켓플레이스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-174">For How tooprovide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common tooall artifacts published in hello Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="d25c3-175">7.    사용자 제공 tooyour 서비스 (SQL Azure 기반 또는 기반 웹 서비스)를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-175">7.    Connect your offer tooyour Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="d25c3-176">Hello 클릭 **데이터 서비스** 하위 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-176">Click on hello **Data Services** sub-menu.</span></span>

<span data-ttu-id="d25c3-177">Hello hello 페이지의 위쪽 절반에 만들라는 메시지가 tooprovide hello 제공 **Namespace**합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-177">On hello upper half of hello page you’ll be asked tooprovide hello offer’s **Namespace**.</span></span>  

  ![drawing](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="d25c3-179">새로 만든 tooexpose 제공 tooAzure 마켓플레이스 게시자 hello 어떻게 hello 아래 질문을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-179">hello below question will define how hello Publisher is going tooexpose newly created offer tooAzure Marketplace.</span></span> <span data-ttu-id="d25c3-180">(자세한 내용은 참조는 hello [데이터 서비스 기술 필수 구성 요소 가이드](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="d25c3-180">(For more details see hello [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![drawing](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="d25c3-182">**Hello 게시 데이터베이스 기반 서비스**</span><span class="sxs-lookup"><span data-stu-id="d25c3-182">**Publishing hello Database based service**</span></span>

<span data-ttu-id="d25c3-183">**데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-183">Click on **Database**.</span></span> <span data-ttu-id="d25c3-184">다음 페이지 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-184">hello following page will appear:</span></span>

  ![drawing](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="d25c3-186">toocreate hello 데이터 집합에 대 한 CSDL 매핑을 hello SQL Azure DB에 따라:</span><span class="sxs-lookup"><span data-stu-id="d25c3-186">toocreate a CSDL mapping for hello Dataset based on hello SQL Azure DB:</span></span>

  ![drawing](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="d25c3-188">그 후 각 테이블에 대해</span><span class="sxs-lookup"><span data-stu-id="d25c3-188">And then for each table</span></span>

  ![그리기](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![그리기](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="d25c3-191">웹 서비스가 다음과 같으면</span><span class="sxs-lookup"><span data-stu-id="d25c3-191">If Web Service</span></span>

  ![drawing](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="d25c3-193">읽기 [CSDL 통해 서비스 tooOData 웹 기존 매핑](marketplace-publishing-data-service-creation-odata-mapping.md) 자세한 지침과 CSDL 웹 서비스를 만들기 위한 예제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-193">Read [Mapping an existing web service tooOData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d25c3-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d25c3-194">Next Steps</span></span>
<span data-ttu-id="d25c3-195">데이터 서비스 제공을 만든 했으므로 hello의 hello 지침을 완료 하는 확인 하십시오 [마켓플레이스 마케팅 콘텐츠 가이드](marketplace-publishing-push-to-staging.md) 계속 하기 전에 너무[준비의데이터서비스테스트](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="d25c3-195">Now that you've created your Data Service offer, please ensure that you complete hello instructions in hello [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward too[Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d25c3-196">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d25c3-196">See Also</span></span>
* [<span data-ttu-id="d25c3-197">시작 하기: 어떻게 toopublish 제안 toohello Azure 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="d25c3-197">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="d25c3-198">이 문서를 읽을 전반적인 OData 매핑 프로세스 및 목적을 이해에서 하려는 경우 hello [데이터 서비스 OData 매핑](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview 정의 구조체 및 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-198">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="d25c3-199">학습 및 이해 hello 특정 노드 및 해당 매개 변수의 하려는 경우이 문서를 읽어 보세요. [데이터 서비스 OData 매핑 노드](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) 정의 및 설명을, 예제 및 사례 컨텍스트 사용에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-199">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="d25c3-200">예를 검토 하려는 경우이 문서를 읽어 보세요. [데이터 서비스 OData 매핑 예제](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee 샘플 코드와 코드 구문 및 컨텍스트를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c3-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com

---
title: "Marketplace용 데이터 서비스 만들기 가이드 | Microsoft Docs"
description: "Azure 마켓플레이스에서 구매하기 위한 데이터 서비스를 만들고 인증하고 배포하는 방법에 대한 자세한 지침입니다."
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
ms.openlocfilehash: c0c9362f1c2e15c947aaaf7187f3383ad243140f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="data-service-publishing-guide-for-the-azure-marketplace"></a><span data-ttu-id="5cf8f-103">Azure 마켓플레이스에 대한 데이터 서비스 게시 가이드</span><span class="sxs-lookup"><span data-stu-id="5cf8f-103">Data Service Publishing Guide for the Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5cf8f-104">**현재는 새 데이터 서비스 게시자 등록을 더 이상 받지 않고 있습니다. 따라서 새 데이터 서비스 등재 승인을 받을 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="5cf8f-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="5cf8f-105">SaaS 비즈니스 응용 프로그램을 AppSource에 게시하려는 경우 [여기](https://appsource.microsoft.com/partners)에서 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="5cf8f-106">IaaS 응용 프로그램 또는 개발자 서비스를 Azure Marketplace에 게시하려는 경우에는 [여기](https://azure.microsoft.com/marketplace/programs/certified/)에서 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="5cf8f-107">1단계 [계정 만들기 및 등록](marketplace-publishing-accounts-creation-registration.md)을 완료한 후 Azure Marketplace에서 제공하는 데이터 서비스 제품의 [일반 비기술 필수 조건](marketplace-publishing-pre-requisites.md) 및 [기술 필수 조건](marketplace-publishing-data-service-creation-prerequisites.md)을 안내해 드렸습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-107">After completing the step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through the [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="5cf8f-108">이제 Azure Marketplace의 [게시 포털][link-pubportal]에서 데이터 서비스 제품을 만드는 단계를 안내해 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-108">Now we will walk you through the steps for creating a Data Service offer on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="1----login-to-the-publishing-portal"></a><span data-ttu-id="5cf8f-109">1.    게시 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-109">1.    Login to the Publishing Portal.</span></span>
<span data-ttu-id="5cf8f-110">[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="5cf8f-110">Go to [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="5cf8f-111">**처음으로 게시 포털에 로그인할 때는 개발자 센터에서 회사의 판매자 프로필이 등록된 계정을 동일하게 사용하세요.**</span><span class="sxs-lookup"><span data-stu-id="5cf8f-111">**For first time login to Publishing Portal, use the same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="5cf8f-112">나중에 게시 포털에서 회사의 직원을 공동 관리자로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-112">(Later you can add any employee of your company as a co-admin in the Publishing Portal).</span></span>

<span data-ttu-id="5cf8f-113">게시 포털에 처음 로그인하는 경우 **데이터 서비스 게시** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-113">Click on the **Publish a Data Services** tile if this is the first login into the publishing portal.</span></span>

## <a name="2----choose-data-services-in-the-navigation-menu-on-the-left-side"></a><span data-ttu-id="5cf8f-114">2.    왼쪽의 탐색 메뉴에서 **Data Services**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-114">2.    Choose **Data Services** in the navigation menu on the left side.</span></span>
  ![drawing](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="5cf8f-116">3.    새 데이터 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="5cf8f-117">새 데이터 서비스 제품의 제목을 입력하고 오른쪽의 “+”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-117">Fill in the title for your new Data Service Offer and click on “+” on the right.</span></span>

  ![drawing](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-the-sub-menu-under-the-newly-created-data-service-in-the-navigation-menu"></a><span data-ttu-id="5cf8f-119">4.    탐색 메뉴에서 새로 만든 데이터 서비스 아래에 있는 하위 메뉴를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-119">4.    Review the sub-menu under the newly created Data Service in the navigation menu.</span></span>
<span data-ttu-id="5cf8f-120">**연습** 탭을 클릭하고 Azure 마켓플레이스에 데이터 서비스를 적절히 게시하는 데 필요한 모든 단계를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-120">Click on the **Walkthrough** tab and review all necessary steps needed to publish properly the Data Service on the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="5cf8f-121">언제든지 "연습" 페이지의 링크를 클릭하거나 왼쪽에서 데이터 서비스 제품 하위 메뉴의 탭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-121">You always can click on the links in the “Walkthrough” page or use tabs on the Data Service offer’s sub-menu on the left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="5cf8f-122">5.    새 플랜을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="5cf8f-123">제품, 플랜, 트랜잭션.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="5cf8f-124">각 제품에 플랜이 여러 개 있어도 되는데, 적어도 플랜이 하나(1) 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="5cf8f-125">최종 사용자는 제품을 구독할 때 제품의 플랜 중 하나를 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-125">When end-users subscribe to your offer they subscribe for one of the offer’s Plan.</span></span> <span data-ttu-id="5cf8f-126">각 플랜은 최종 사용자가 서비스를 이용할 수 있는 방식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-126">Each plan defines how end-users will be able to use your service.</span></span>

<span data-ttu-id="5cf8f-127">현재 Azure Marketplace는 데이터 서비스에 대한 월간 구독 트랜잭션 기반 모델만 지원합니다. 즉, 최종 사용자는 구독하는 특정 플랜의 가격에 따른 월정액 요금제에서 청구되는 요금을 지불하며, 매월 플랜에 정의된 수만큼의 트랜잭션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according to the price of the specific plan they subscribed to and will be able to consume each month number of transaction defined by the plan.</span></span>

<span data-ttu-id="5cf8f-128">일반적으로 각 트랜잭션은 서비스로 전송되는 쿼리를 기준으로 데이터 서비스에서 반환하는 레코드 수로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-128">Each Transaction usually defined as number of records your Data Service will return based on the query sent to the Service.</span></span> <span data-ttu-id="5cf8f-129">기본값은 100입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-129">The default is 100.</span></span> <span data-ttu-id="5cf8f-130">각 쿼리로 반환되는 트랜잭션 수는 레코드 수를 100으로 나눈 값을 가장 가까운 정수로 반올림한 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-130">Number of transactions returned to each query will be number of records divided by 100 and rounded up to the closest integer.</span></span>

<span data-ttu-id="5cf8f-131">각 쿼리에서 사용한 트랜잭션 수를 모니터링(측정)하는 것은 Azure 마켓플레이스 서비스 계층의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-131">It’s Azure Marketplace Service layer responsibility to monitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5cf8f-132">한 달이 지나기 전에 트랜잭션 제한에 도달한 최종 사용자는 월간 구독 주기가 끝날 때까지 서비스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-132">End-Users which reached the transaction limit during the month will be blocked from continuing to use the service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="5cf8f-133">플랜 또는 플랜 중 하나에 무제한 트랜잭션을 포함할 수 있습니다(필수는 아님).</span><span class="sxs-lookup"><span data-stu-id="5cf8f-133">The plan or one of the plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="5cf8f-134">플랜을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-134">Create a plan.</span></span>
1. <span data-ttu-id="5cf8f-135">“새 플랜 추가” 옆에 있는 **“+”** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-135">Click on **“+”** next to the “Add a new plan”.</span></span>
2. <span data-ttu-id="5cf8f-136">이 플랜의 사용량을 **무제한** 또는 **제한** 중에 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-136">Choose one of the options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="5cf8f-137">제한을 선택할 경우 한 달 동안 플랜에 허용되는 트랜잭션 수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-137">If Limited then provide the number of transaction the plan will allow to consume in a month.</span></span>
   
    ![drawing](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="5cf8f-139">또한 게시 포털에서 "플랜 식별자"를 제안할 것입니다. 플랜 식별자는 UI에서 최종 사용자에 플랜 이름을 알려주고 마켓플레이스 서비스가 플랜을 식별하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-139">Publishing Portal will also suggest “Plan Identifier”, which will be used to communicate to the end-users the name of the plan in the UI and also used by the Market Place Service to identify the Plan.</span></span> <span data-ttu-id="5cf8f-140">원하는 경우 "플랜 식별자"를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-140">You can change the “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5cf8f-141">"플랜 식별자"는 각 제품의 범위 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-141">The “Plan Identifier” must be unique within the scope of each offer.</span></span> <span data-ttu-id="5cf8f-142">게시 포털에서 여러 가지 식별자가 사용되기 때문에 프로덕션에 처음으로 게시한 후 플랜 식별자가 잠기게 되고 더 이상 이 식별자를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-142">As many other Identifiers used in the Publishing Portal Plan identifier will be locked after the first publishing to production and you will not be able to change this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="5cf8f-143">클릭하여 선택한 내용을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-143">Click to accept your choice.</span></span>
4. <span data-ttu-id="5cf8f-144">새로 만든 플랜에 대한 몇 가지 추가 질문을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![그리기](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="5cf8f-146">질문</span><span class="sxs-lookup"><span data-stu-id="5cf8f-146">Question</span></span> | <span data-ttu-id="5cf8f-147">중요도</span><span class="sxs-lookup"><span data-stu-id="5cf8f-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="5cf8f-148">**이 계획은 무료이며 전 세계에서 사용할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="5cf8f-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="5cf8f-149">완전 무료 플랜을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="5cf8f-150">이 제품의 유일한 플랜인 경우 마켓플레이스에 "무료 제품"을 게시한다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-150">If it’s the only plan for this offer – it means that you are publishing “Free Offer” in the Marketplace.</span></span> <span data-ttu-id="5cf8f-151">플랜 중 하나만 무료인 경우 월별 트랜잭션 수가 상대적으로 적은 서비스에 대해 자세히 알아보도록 최종 사용자에게 제안하는 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-151">If it’s only for one (of few) Plan, the it gives you an option to offer end-users to learn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="5cf8f-152">"예"라고 대답하면 더 이상 질문이 나오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-152">If the answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="5cf8f-153">최종 사용자는 언제든지 유료 플랜으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-153">End users can always upgrade to the paid plans.</span></span>
> 
> 

| <span data-ttu-id="5cf8f-154">질문</span><span class="sxs-lookup"><span data-stu-id="5cf8f-154">Question</span></span> | <span data-ttu-id="5cf8f-155">중요도</span><span class="sxs-lookup"><span data-stu-id="5cf8f-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="5cf8f-156">**무료 평가판이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="5cf8f-156">**Is free trial available?**</span></span> |<span data-ttu-id="5cf8f-157">“평가판 없음”을 선택할 수도 있고 “1개월” 동안 플랜을 사용할 수 있는 옵션을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-157">You can choose between “No Trial” at all or give an option to use your Plan for “One Month”.</span></span> <span data-ttu-id="5cf8f-158">게시자는 최종 사용자가 1개월 동안 플랜을 무료로 사용하면서 제품의 장점을 이해할 수 있는 기회를 제공하기 위해 이 옵션을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-158">Publishers like to use this option to provide end-users the possibility to understand the benefits of the offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="5cf8f-159">최종 사용자는 신용 카드, 기업 계약 등의 결제 수단을 설정해야만 무료 평가판을 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-159">End-users will only be able to purchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="5cf8f-160">고객이 구독 취소 절차를 시작하지 않는 한, 1개월 무료 평가판 기간이 끝나면 Azure Marketplace에서는 구독 날짜를 기준으로 고객에게 요금을 부과합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-160">After one month of the free trial, Azure Marketplace will start charging customers the price as of the date of the subscription, unless the customer initiated the subscription cancellation.</span></span> <span data-ttu-id="5cf8f-161">최종 사용자에게 특별한 알림이 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-161">No special notification will be provided to the end-users.</span></span>
> 
> 

| <span data-ttu-id="5cf8f-162">질문</span><span class="sxs-lookup"><span data-stu-id="5cf8f-162">Question</span></span> | <span data-ttu-id="5cf8f-163">중요도</span><span class="sxs-lookup"><span data-stu-id="5cf8f-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="5cf8f-164">**이 플랜을 구매하려면 프로모션 코드가 필요합니까?**</span><span class="sxs-lookup"><span data-stu-id="5cf8f-164">**This plan requires a promotion code to purchase?**</span></span> |<span data-ttu-id="5cf8f-165">게시자는 특정 고객에게 "Promocode"라는 특수 코드를 제공하여 서비스 플랜에 대한 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-165">Publishers have an option to limit access to their Service Plans by providing a special code, called “A Promocode” to specific customers.</span></span> <span data-ttu-id="5cf8f-166">이 Promocode가 있는 최종 사용자만 플랜을 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-166">Only end-users which will have this Promocode will be able to subscribe to the Plan.</span></span> <span data-ttu-id="5cf8f-167">"아니요"를 선택할 경우 제품이 제공되는 지역의 모든 사람이(자세한 내용은 [마켓플레이스 마케팅 콘텐츠 가이드](marketplace-publishing-push-to-staging.md) 참조) 이 플랜을 구독할 수 있다고 동의하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-167">If you choose “No”, then you agree that everyone from the region where the offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able to subscribe to this plan.</span></span> <span data-ttu-id="5cf8f-168">더 이상 질문이 나오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="5cf8f-169">**유효한 프로모션 코드가 없는 사용자에게도 이 플랜을 숨길까요?**</span><span class="sxs-lookup"><span data-stu-id="5cf8f-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="5cf8f-170">이전 질문에 "예"라고 대답했으면 마켓플레이스 UI에서 이 플랜을 완전히 제거하는 옵션이 게시자에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-170">If the answer to the previous question is “Yes” the Publisher has an option to completely remove this plan from appearing in the UI of the Marketplace.</span></span> <span data-ttu-id="5cf8f-171">다시 말해서 고객이 제품 세부 정보 페이지에서 이 플랜을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-171">It means, customers will not see this plan in the Offer’s details page.</span></span> <span data-ttu-id="5cf8f-172">플랜 구매를 위한 promocode를 받은 최종 사용자는 이 promocode를 사용하여 플랜을 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-172">End-users which will receive a promocode to purchase it, will be able to subscribe to it using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="5cf8f-173">6.    마켓플레이스 마케팅 콘텐츠를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="5cf8f-174">**마케팅, 가격 책정, 지원 및 범주** 탭의 필수 정보를 입력하는 방법은 Azure 마켓플레이스에 게시된 모든 아티팩트에 공통적으로 적용되는 [마켓플레이스 마케팅 콘텐츠 가이드](marketplace-publishing-push-to-staging.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-174">For How to provide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common to all artifacts published in the Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-to-your-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="5cf8f-175">7.    제품을 서비스(SQL Azure 기반 또는 웹 서비스 기반)에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-175">7.    Connect your offer to your Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="5cf8f-176">**데이터 서비스** 하위 메뉴를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-176">Click on the **Data Services** sub-menu.</span></span>

<span data-ttu-id="5cf8f-177">페이지의 위쪽 절반에서 제품의 **네임스페이스**를 입력하라고 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-177">On the upper half of the page you’ll be asked to provide the offer’s **Namespace**.</span></span>  

  ![그리기](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="5cf8f-179">아래 질문은 게시자가 새로 만든 제품을 Azure 마켓플레이스에 노출하는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-179">The below question will define how the Publisher is going to expose newly created offer to Azure Marketplace.</span></span> <span data-ttu-id="5cf8f-180">자세한 내용은 [데이터 서비스 기술 필수 조건 가이드](marketplace-publishing-data-service-creation-prerequisites.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-180">(For more details see the [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![그리기](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="5cf8f-182">**데이터베이스 기반 서비스 게시**</span><span class="sxs-lookup"><span data-stu-id="5cf8f-182">**Publishing the Database based service**</span></span>

<span data-ttu-id="5cf8f-183">**데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-183">Click on **Database**.</span></span> <span data-ttu-id="5cf8f-184">다음 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-184">The following page will appear:</span></span>

  ![그리기](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="5cf8f-186">SQL Azure DB를 기반으로 데이터 집합에 대한 CSDL 매핑을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="5cf8f-186">To create a CSDL mapping for the Dataset based on the SQL Azure DB:</span></span>

  ![그리기](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="5cf8f-188">그 후 각 테이블에 대해</span><span class="sxs-lookup"><span data-stu-id="5cf8f-188">And then for each table</span></span>

  ![그리기](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![그리기](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="5cf8f-191">웹 서비스가 다음과 같으면</span><span class="sxs-lookup"><span data-stu-id="5cf8f-191">If Web Service</span></span>

  ![그리기](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="5cf8f-193">[CSDL을 통해 기존 서비스를 OData에 매핑](marketplace-publishing-data-service-creation-odata-mapping.md) 을 읽고 CSDL 웹 서비스를 만드는 방법에 대한 지침과 예를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-193">Read [Mapping an existing web service to OData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5cf8f-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5cf8f-194">Next Steps</span></span>
<span data-ttu-id="5cf8f-195">데이터 서비스 제품을 만들었으니, 이제 [마켓플레이스 마케팅 콘텐츠 가이드](marketplace-publishing-push-to-staging.md)의 지침을 완료한 후 [스테이징에서 데이터 서비스 테스트](marketplace-publishing-data-service-test-in-staging.md)를 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-195">Now that you've created your Data Service offer, please ensure that you complete the instructions in the [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward to [Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5cf8f-196">참고 항목</span><span class="sxs-lookup"><span data-stu-id="5cf8f-196">See Also</span></span>
* [<span data-ttu-id="5cf8f-197">시작: Azure 마켓플레이스에 제품을 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="5cf8f-197">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="5cf8f-198">전체 OData 매핑 프로세스와 목적을 이해하려는 경우 문서 [데이터 서비스 OData 매핑](marketplace-publishing-data-service-creation-odata-mapping.md) 을 읽고 정의, 구조 및 지침을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-198">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="5cf8f-199">특정 노드 및 해당 매개 변수를 학습하고 이해하려면 문서 [데이터 서비스 OData 매핑 노드](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) 에서 정의 및 설명, 예제, 사용 사례 컨텍스트를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-199">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="5cf8f-200">예제를 검토하고 싶으면 [데이터 서비스 OData 매핑 예제](marketplace-publishing-data-service-creation-odata-mapping-examples.md) 문서를 통해 샘플 코드를 살펴보고 코드 구문 및 컨텍스트를 이해하세요.</span><span class="sxs-lookup"><span data-stu-id="5cf8f-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com

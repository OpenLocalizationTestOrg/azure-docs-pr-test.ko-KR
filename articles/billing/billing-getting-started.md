---
title: "aaaPrevent 예상치 못한 비용 청구-Azure 관리 | Microsoft Docs"
description: "자세한 내용은 방법 tooavoid, Azure 청구서에 예기치 않은 요금입니다. Microsoft Azure 구독에 대한 비용 추적 및 관리 기능을 사용합니다."
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
experimental_id: a2b2579c-cd2e-41
ms.openlocfilehash: 4827c65a55fe953c329ab26cc4e882266073c60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-costs-with-azure-billing-and-cost-management"></a><span data-ttu-id="ecb3e-104">Azure 청구 및 비용 관리를 사용하여 예상치 못한 비용 방지</span><span class="sxs-lookup"><span data-stu-id="ecb3e-104">Prevent unexpected costs with Azure billing and cost management</span></span>

<span data-ttu-id="ecb3e-105">Azure에 등록할 때 몇 가지 방법으로 사용자 지출 잘 알 tooget를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-105">When you sign up for Azure, there are several things you can do tooget a better idea of your spend.</span></span> <span data-ttu-id="ecb3e-106">Hello에 [Azure 포털](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)hello 구독을 선택 하는 경우 현재 비용 분석을 사용 하 여 확인 하 고 진행 속도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-106">In hello [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), when you select hello subscription, you can see your current cost breakdown and burn rate.</span></span> <span data-ttu-id="ecb3e-107">[과거 송장 및 자세한 사용 현황 파일도 다운로드](billing-download-azure-invoice-daily-usage-date.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-107">You can also [download past invoices and detail usage files](billing-download-azure-invoice-daily-usage-date.md).</span></span> <span data-ttu-id="ecb3e-108">서로 다른 프로젝트 또는 팀에 사용 되는 리소스에 대 한 toogroup 비용을 원하는 경우 확인 [리소스 태그 지정](../azure-resource-manager/resource-group-using-tags.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-108">If you want toogroup costs for resources used for different projects or teams, look at [resource tagging](../azure-resource-manager/resource-group-using-tags.md).</span></span> <span data-ttu-id="ecb3e-109">조직에 toouse 선호 하는 보고 시스템을 체크 아웃 hello [Api 청구](billing-usage-rate-card-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-109">If your organization has a reporting system that you prefer toouse, check out hello [billing APIs](billing-usage-rate-card-overview.md).</span></span> 

<span data-ttu-id="ecb3e-110">일간 사용 현황에 대한 자세한 내용은 [Microsoft Azure 청구서 이해](billing-understand-your-bill.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-110">For more information about your daily usage, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span>

<span data-ttu-id="ecb3e-111">EA (기업 계약), 클라우드 솔루션 공급자 (CSP) 또는 Azure 스폰서쉽을 통해 구독이 있는 경우이 문서에 많은 기능 tooyou를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-111">If your subscription is through an Enterprise Agreement (EA), Cloud Solution Provider (CSP), or Azure Sponsorship, then many features in this article don't apply tooyou.</span></span> <span data-ttu-id="ecb3e-112">대신 비용 관리에 사용할 수 있는 다른 도구 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-112">Instead, we have a different set of tools that you can use for cost management.</span></span> <span data-ttu-id="ecb3e-113">See [EA, CSP 및 스폰서쉽에 대한 추가 리소스](#other-offers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-113">See [Additional resources for EA, CSP, and Sponsorship](#other-offers).</span></span>

<span data-ttu-id="ecb3e-114">가입 되어 무료 평가판을 [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)열기 (AIO) 또는 BizSpark, Azure, 다음에 대 한 자세한 내용은 [지출 한도](#spending-limit) tooavoid unexpectantly 사용 하지 않도록 설정 하 여 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-114">If your subscription is a Free Trial, [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure in Open (AIO), or BizSpark, then learn about [spending limits](#spending-limit) tooavoid having your subscription unexpectantly disabled.</span></span> 

## <a name="day-0-before-you-add-azure-services"></a><span data-ttu-id="ecb3e-115">0일차: Azure 서비스를 추가하기 전에</span><span class="sxs-lookup"><span data-stu-id="ecb3e-115">Day 0: Before you add Azure services</span></span>

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a><span data-ttu-id="ecb3e-116">예상 비용 온라인 hello 가격 계산기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ecb3e-116">Estimate cost online using hello pricing calculator</span></span>

<span data-ttu-id="ecb3e-117">체크 아웃 hello [가격 계산기](https://azure.microsoft.com/pricing/calculator/) 및 [총 비용 소유권 계산기의](https://aka.ms/azure-tco-calculator) tooget에 관심이 hello 서비스는 예상 hello 월별 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-117">Check out hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/) and [total cost of ownership calculator](https://aka.ms/azure-tco-calculator) tooget an estimate hello monthly cost of hello service you're interested in.</span></span> <span data-ttu-id="ecb3e-118">예를 들어 A1 Windows 가상 컴퓨터 (VM)은 예상된 toocost hello 전체 시간에 실행 파일을 그대로 둘 경우 $66.96 USD/월에 시간 계산입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-118">For example, an A1 Windows Virtual Machine (VM) is estimated toocost $66.96 USD/month in compute hours if you leave it running hello whole time:</span></span>

![Hello 가격 계산기 A1 Windows VM 매달 예상된 toocost $66.96 USD 임을 보여 주는 스크린샷](./media/billing-getting-started/pricing-calcVM.png)

<span data-ttu-id="ecb3e-120">자세한 내용은 [가격 책정 FAQ](https://azure.microsoft.com/pricing/faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-120">For more information, see [pricing FAQ](https://azure.microsoft.com/pricing/faq/).</span></span> <span data-ttu-id="ecb3e-121">또는 tootalk tooa 사람 1-800-867-1389를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-121">Or if you want tootalk tooa person, call 1-800-867-1389.</span></span>

### <a name="check-your-subscription-and-access"></a><span data-ttu-id="ecb3e-122">구독 및 액세스 권한 확인</span><span class="sxs-lookup"><span data-stu-id="ecb3e-122">Check your subscription and access</span></span>

<span data-ttu-id="ecb3e-123">보기 비용 필요 [구독 액세스 toobilling 정보](billing-manage-access.md), 계정 관리자만 hello hello에 액세스할 수 있지만 [r e 계정 센터](https://account.windowsazure.com/Home/Index), 대금 청구 정보를 변경 하 고 구독을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-123">Viewing costs require [subscriptions-level access toobilling information](billing-manage-access.md), but only hello Account admin can access hello [Account Center](https://account.windowsazure.com/Home/Index), change billing info, and manage subscriptions.</span></span> <span data-ttu-id="ecb3e-124">admin 님 안녕하세요 계정은 hello 등록 프로세스 진행 hello 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-124">hello Account admin is hello person who went through hello sign-up process.</span></span> <span data-ttu-id="ecb3e-125">자세한 내용은 참조 [hello 구독 또는 서비스를 관리 하는 Azure 관리자 역할을 추가 또는 변경](billing-add-change-azure-subscription-administrator.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-125">For more information, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="ecb3e-126">toosee 계정 관리자 hello 하는 경우 이동 toohello [hello Azure 포털에서에서 구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) hello 목록에 액세스할 수 있는 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-126">toosee if you're hello Account admin, go toohello [Subscriptions blade in hello Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) and look at hello list of subscriptions you have access to.</span></span> <span data-ttu-id="ecb3e-127">**내 역할** 아래에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-127">Look under **My Role**.</span></span> <span data-ttu-id="ecb3e-128">*계정 관리자*가 표시되면 문제가 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-128">If it says *Account admin*, then you're ok.</span></span> <span data-ttu-id="ecb3e-129">*소유자* 등이 표시되면 모든 권한이 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-129">If it says something else like *Owner*, then you don't have full privileges.</span></span>

![Hello hello Azure 포털에서에서 구독 보기의에서 사용자 역할의 스크린 샷](./media/billing-getting-started/sub-blade-view.PNG)

<span data-ttu-id="ecb3e-131">계정 관리자 hello 하지 하는 경우 다른 사람이 아마도 제공한 통해 부분적인 액세스 권한을 [Azure Active Directory 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="ecb3e-131">If you're not hello Account admin, then somebody probably gave you partial access via [Azure Active Directory Role-based Access Control](../active-directory/role-based-access-control-configure.md) (RBAC).</span></span> <span data-ttu-id="ecb3e-132">toomanage 구독 및 청구 정보를 변경 [계정 admin 님 안녕하세요 찾을](billing-subscription-transfer.md#whoisaa) tooperform hello 작업을 요청 하십시오 또는 [hello 구독 tooyou 전송](billing-subscription-transfer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-132">toomanage subscriptions and change billing info, [find hello Account admin](billing-subscription-transfer.md#whoisaa) and ask them tooperform hello tasks or [transfer hello subscription tooyou](billing-subscription-transfer.md).</span></span>

<span data-ttu-id="ecb3e-133">계정 관리자는 더 이상 사용자의 조직과 toomanage 요금 청구서 주소, 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-133">If your Account admin is no longer with your organization and you need toomanage billing, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> 

### <span data-ttu-id="ecb3e-134"><a name="spending-limit"></a> 지출 한도가 설정되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="ecb3e-134"><a name="spending-limit"></a> Check if you have a spending limit on</span></span>

<span data-ttu-id="ecb3e-135">크레딧을 사용 하는 구독을 사용 하는 경우 다음 hello 지출 한도 대해 켜져 있습니다 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-135">If you have a subscription that uses credits, then hello spending limit is turned on for you by default.</span></span> <span data-ttu-id="ecb3e-136">이러한 방식으로 모든 크레딧을 지출하면 신용 카드에 요금이 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-136">This way, when you spend all your credits, your credit card doesn't get charged.</span></span> <span data-ttu-id="ecb3e-137">Hello 참조 [전체 목록은 Azure 혜택 및 지출 한도의 가용성을 hello](https://azure.microsoft.com/support/legal/offer-details/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-137">See hello [full list of Azure offers and hello availability of spending limit](https://azure.microsoft.com/support/legal/offer-details/).</span></span>

<span data-ttu-id="ecb3e-138">그러나 지출 한도에 도달하면 서비스는 사용되지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-138">However, if you hit your spending limit, your services get disabled.</span></span> <span data-ttu-id="ecb3e-139">즉, VM이 할당 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-139">That means your VMs are deallocated.</span></span> <span data-ttu-id="ecb3e-140">tooavoid 서비스 가동 중지 시간이 꺼야 hello 지출 한도입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-140">tooavoid service downtime, you must turn off hello spending limit.</span></span> <span data-ttu-id="ecb3e-141">초과분이 파일의 신용 카드에 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-141">Any overage gets charged onto your credit card on file.</span></span> 

<span data-ttu-id="ecb3e-142">하 한 (를) 가져왔습니다 지출 한도를 경우 toosee 이동 toohello [구독 보기는 hello r e 계정 센터에서에서](https://account.windowsazure.com/Subscriptions)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-142">toosee if you've got spending limit on, go toohello [Subscriptions view in hello Account Center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="ecb3e-143">지출 한도가 켜져 있으면 배너가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-143">A banner appears if your spending limit is on:</span></span>

![지출 한도 hello r e 계정 센터에 있는 것에 대 한 경고를 보여 주는 스크린샷](./media/billing-getting-started/spending-limit-banner.PNG)

<span data-ttu-id="ecb3e-145">Hello 배너를 클릭 하 고 프롬프트 tooremove hello 지출 한도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-145">Click hello banner and follow prompts tooremove hello spending limit.</span></span> <span data-ttu-id="ecb3e-146">등록할 때 신용 카드 정보를 입력 하지 않은 tooremove hello 지출 한도 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-146">If you didn't enter credit card information when you signed up, you must enter it tooremove hello spending limit.</span></span> <span data-ttu-id="ecb3e-147">자세한 내용은 참조 [Azure 지출 한도-작동 방식과 tooenable 제거](https://azure.microsoft.com/pricing/spending-limits/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-147">For more information, see [Azure spending limit – How it works and how tooenable or remove it](https://azure.microsoft.com/pricing/spending-limits/).</span></span>

### <a name="set-up-billing-alerts"></a><span data-ttu-id="ecb3e-148">청구 경고 설정</span><span class="sxs-lookup"><span data-stu-id="ecb3e-148">Set up billing alerts</span></span>

<span data-ttu-id="ecb3e-149">청구 경고 설정 tooget 전자 메일 사용 비용 지정 하는 금액을 초과 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-149">Set up billing alerts tooget emails when your usage costs exceed an amount that you specify.</span></span> <span data-ttu-id="ecb3e-150">월별 크레딧이 있는 경우 지정된 금액을 다 사용하는 경우에 대해 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-150">If you have monthly credits, set up alerts for when you use up a specified amount.</span></span> <span data-ttu-id="ecb3e-151">자세한 내용은 [Microsoft Azure 구독에 대한 청구 경고 설정](billing-set-up-alerts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-151">For more information, see [Set up billing alerts for your Microsoft Azure subscriptions](billing-set-up-alerts.md).</span></span>

![청구 경고 전자 메일 스크린 샷](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> <span data-ttu-id="ecb3e-153">이 기능은 미리 보기 상태이므로 정기적으로 사용 현황을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-153">This feature is still in preview so you should check your usage regularly.</span></span>

<span data-ttu-id="ecb3e-154">Toouse hello hello 첫 번째 경고에 대 한 지침으로 가격 계산기에서에서 예상 비용을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-154">You might want toouse hello cost estimate from hello pricing calculator as a guideline for your first alert.</span></span>

### <a name="understand-limits-and-quotas-for-your-subscription"></a><span data-ttu-id="ecb3e-155">구독에 대한 한도 및 할당량 이해</span><span class="sxs-lookup"><span data-stu-id="ecb3e-155">Understand limits and quotas for your subscription</span></span>

<span data-ttu-id="ecb3e-156">Hello CPU 코어 수와 IP 주소 등을 위한 tooeach 구독은 기본 제한.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-156">There are default limits tooeach subscription for things like hello number of CPU cores and IP addresses.</span></span> <span data-ttu-id="ecb3e-157">이러한 한도에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-157">Be mindful of these limits.</span></span> <span data-ttu-id="ecb3e-158">자세한 내용은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-158">For more information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="ecb3e-159">증가 tooyour 제한 또는 할당량을 요청할 수 [지원 팀에 연락](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-159">You can request an increase tooyour limit or quota by [contacting support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="day-1-as-you-add-services"></a><span data-ttu-id="ecb3e-160">1일차: 서비스 추가 시</span><span class="sxs-lookup"><span data-stu-id="ecb3e-160">Day 1: As you add services</span></span>

### <a name="review-hello-estimated-cost-in-hello-portal"></a><span data-ttu-id="ecb3e-161">검토 hello 예상 비용 hello 포털에서</span><span class="sxs-lookup"><span data-stu-id="ecb3e-161">Review hello estimated cost in hello portal</span></span>

<span data-ttu-id="ecb3e-162">일반적으로 hello Azure 포털에서에서 서비스를 추가 하면 매달 유사한 예상된 비용을 표시 하는 보기는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-162">Typically when you add a service in hello Azure portal, there's a view that shows you a similar estimated cost per month.</span></span> <span data-ttu-id="ecb3e-163">예를 들어 Windows VM의 hello 크기를 선택 하면 hello hello 계산 시간에 대 한 월별 비용을 예상 표시:</span><span class="sxs-lookup"><span data-stu-id="ecb3e-163">For example, when you choose hello size of your Windows VM you see hello estimated monthly cost for hello compute hours:</span></span>

![예: A1 Windows VM은 매달 예상된 toocost $66.96 USD](./media/billing-getting-started/vm-size-cost.PNG)

### <span data-ttu-id="ecb3e-165"><a name="tags"></a>태그 tooyour 리소스 toogroup 청구 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="ecb3e-165"><a name="tags"></a> Add tags tooyour resources toogroup your billing data</span></span>

<span data-ttu-id="ecb3e-166">지원 되는 서비스에 대 한 태그 toogroup 청구 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-166">You can use tags toogroup billing data for supported services.</span></span> <span data-ttu-id="ecb3e-167">예를 들어 서로 다른 팀에 대 한 여러 Vm을 실행 하는 경우 태그 toocategorize 비용 비용 센터 (마케팅, 재무 HR) 또는 (프로덕션, 사전 프로덕션 테스트) 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-167">For example, if you run several VMs for different teams, then you can use tags toocategorize costs by cost center (HR, marketing, finance) or environment (production, pre-production, test).</span></span> 

![Hello 포털에 태그를 설정을 보여 주는 스크린샷](./media/billing-getting-started/tags.PNG)

<span data-ttu-id="ecb3e-169">hello 태그가 서로 다른 비용이 보고 보기에서 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-169">hello tags show up throughout different cost reporting views.</span></span> <span data-ttu-id="ecb3e-170">예를 들어 지금 바로 [비용 분석 보기](#costs)에 표시되거나 첫 번째 청구 기간 후에 [상세 사용 현황 .csv](#invoice-and-usage)에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-170">For example, they're visible in your [cost analysis view](#costs) right away and [detail usage .csv](#invoice-and-usage) after your first billing period.</span></span>

<span data-ttu-id="ecb3e-171">자세한 내용은 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](../azure-resource-manager/resource-group-using-tags.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-171">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a><span data-ttu-id="ecb3e-172">VM에 대한 자동 종료와 같은 비용 절감에 기능 사용 고려</span><span class="sxs-lookup"><span data-stu-id="ecb3e-172">Consider enabling cost-cutting features like auto-shutdown for VMs</span></span>

<span data-ttu-id="ecb3e-173">시나리오에 따라 hello Azure 포털에서에서 Vm에 대 한 자동 종료를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-173">Depending on your scenario, you could configure auto-shutdown for your VMs in hello Azure portal.</span></span> <span data-ttu-id="ecb3e-174">자세한 내용은 [Azure Resource Manager를 사용한 VM에 대한 자동 종료](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-174">For more information, see [Auto-shutdown for VMs using Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).</span></span>

![Hello 포털에서 자동 종료 옵션의 스크린 샷](./media/billing-getting-started/auto-shutdown.PNG)

<span data-ttu-id="ecb3e-176">자동 종료 내에서 종료 하면 VM 전원 옵션으로 hello와 같을 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-176">Auto-shutdown isn't hello same as when you shut down within hello VM with power options.</span></span> <span data-ttu-id="ecb3e-177">자동 종료 중지 하 고 자세한 사용 요금 Vm toostop 할당을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-177">Auto-shutdown stops and deallocates your VMs toostop additional usage charges.</span></span> <span data-ttu-id="ecb3e-178">자세한 내용은 VM 상태에 대한 [Linux VM](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) 및 [Windows VM](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)의 가격 책정 FAQ를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-178">For more information, see pricing FAQ for [Linux VMs](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) and [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) about VM states.</span></span>

<span data-ttu-id="ecb3e-179">개발 및 테스트 환경에 대한 추가 비용 절감에 기능에 대해서는 [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-179">For more cost-cutting features for your development and test environments, check out [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).</span></span>

## <span data-ttu-id="ecb3e-180"><a name="cost-reporting"></a> 2일차 이후: 서비스를 사용한 후 사용 현황 보기</span><span class="sxs-lookup"><span data-stu-id="ecb3e-180"><a name="cost-reporting"></a> Day 2+: After using services, view usage</span></span>

### <span data-ttu-id="ecb3e-181"><a name="costs"></a>정기적으로 hello 비용 분석 포털에서 확인 및 진행 속도</span><span class="sxs-lookup"><span data-stu-id="ecb3e-181"><a name="costs"></a> Regularly check hello portal for cost breakdown and burn rate</span></span>

<span data-ttu-id="ecb3e-182">서비스가 실행 중일 때 부과되는 요금을 정기적으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-182">After you get your services running, regularly check how much they're costing you.</span></span> <span data-ttu-id="ecb3e-183">Hello 현재 볼 수 있습니다 지출 및 Azure 포털에서 진행 되는 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-183">You can see hello current spend and burn rate in Azure portal.</span></span> 

1. <span data-ttu-id="ecb3e-184">Hello 방문 [Azure 포털에서 구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-184">Visit hello [Subscriptions blade in Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

2. <span data-ttu-id="ecb3e-185">Toosee 원하는 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-185">Select your subscription you want toosee.</span></span> <span data-ttu-id="ecb3e-186">하나의 tooselect만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-186">You might only have one tooselect.</span></span>

3. <span data-ttu-id="ecb3e-187">Hello 비용 분석 결과 볼 하 고 hello 팝업 블레이드에서 진행 속도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-187">You should see hello cost breakdown and burn rate in hello popup blade.</span></span> <span data-ttu-id="ecb3e-188">(Hello 맨 위 근처에 경고가 표시는) 자신의 구독에 지원 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-188">It may not be supported for your offer (a warning would be displayed near hello top).</span></span> <span data-ttu-id="ecb3e-189">데이터 toopopulate hello에 대 한 서비스를 추가한 후 24 시간 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-189">Wait 24 hours after you add a service for hello data toopopulate.</span></span>
    
    ![진행 속도 및 hello Azure 포털에서에서 분할의 스크린 샷](./media/billing-getting-started/burn-rate.PNG)

4. <span data-ttu-id="ecb3e-191">Toopin hello view tooyour 대시보드를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-191">You might want toopin hello view tooyour dashboard.</span></span>

    ![보기 toohello 대시보드에 고정 스크린 샷](./media/billing-getting-started/pin.PNG)

5. <span data-ttu-id="ecb3e-193">클릭 **비용 분석** hello 목록 toohello 왼쪽된 toosee hello 비용 별로 분석 리소스에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-193">Click **Cost analysis** in hello list toohello left toosee hello cost breakdown by resource.</span></span>

    ![Azure 포털에서 hello 비용 분석 보기의 스크린샷](./media/billing-getting-started/cost-analysis.PNG)

6. <span data-ttu-id="ecb3e-195">[태그](#tags), 리소스 그룹 및 시간 간격 등의 다양한 속성별로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-195">You can filter by different properties like [tags](#tags), resource group, and timespan.</span></span> <span data-ttu-id="ecb3e-196">클릭 **적용** tooconfirm hello 필터 및 **다운로드** tooexport hello tooa 쉼표로 구분 된 값 (.csv) 파일 보기.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-196">Click **Apply** tooconfirm hello filters and **Download** tooexport hello view tooa Comma-Separated Values (.csv) file.</span></span>

7. <span data-ttu-id="ecb3e-197">자원을 toosee 지출 기록과 얼마나 것 된 비용 계산 하면 각 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-197">Click a resource toosee spend history and how much it was costing you each day.</span></span>

    ![Hello 스크린샷 지출 Azure 포털에서 기록 보기](./media/billing-getting-started/costhistory.PNG)

<span data-ttu-id="ecb3e-199">Hello 비용 hello 예상치 hello 서비스 선택한 때 참조를 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-199">We recommend that you check hello costs you see with hello estimates you saw when you selected hello services.</span></span> <span data-ttu-id="ecb3e-200">Hello 비용 예측에서 크게 다른 경우 리소스에 대해 선택한 계획 (A1 vs A0 VM 예를 들어) 가격 hello를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-200">If hello costs wildly differ from estimates, double check hello pricing plan (A1 vs A0 VM, for example) that you've selected for your resources.</span></span> 

#### <a name="view-costs-for-all-your-subscriptions-in-hello-billing-blade"></a><span data-ttu-id="ecb3e-201">결제 블레이드 hello에서에서 모든 구독에 대 한 비용 보기</span><span class="sxs-lookup"><span data-stu-id="ecb3e-201">View costs for all your subscriptions in hello Billing blade</span></span>

<span data-ttu-id="ecb3e-202">Hello에서 모든 구독에 대 한 hello 집계 청구 금액 및 분석 계정 관리자 hello 처럼 여러 구독을 관리 하는 경우 볼 수 있습니다 [결제 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-202">If you manage multiple subscriptions as hello Account admin, you can see hello aggregate bill amount and breakdown for all your subscriptions in hello [Billing blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade).</span></span> 

<!-- Add screenshots of multiple subs each with billed usage -->

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a><span data-ttu-id="ecb3e-203">Azure Advisor 권장 지침 설정 및 확인</span><span class="sxs-lookup"><span data-stu-id="ecb3e-203">Turn on and check out Azure Advisor recommendations</span></span>

<span data-ttu-id="ecb3e-204">[Azure Advisor](../advisor/advisor-overview.md)는 사용량이 낮은 리소스를 식별하여 비용을 절감하는 데 도움을 주는 미리 보기 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-204">[Azure Advisor](../advisor/advisor-overview.md) is a preview feature that helps you reduce costs by identifying resources with low usage.</span></span> <span data-ttu-id="ecb3e-205">켜십시오 hello Azure 포털에서:</span><span class="sxs-lookup"><span data-stu-id="ecb3e-205">Turn it on in hello Azure portal:</span></span>

![Azure Portal의 Azure Advisor 단추 스크린 샷](./media/billing-getting-started/advisor-button.PNG)

<span data-ttu-id="ecb3e-207">그런 다음 권장 hello에 볼 수 있습니다 **비용** hello 관리자 대시보드 탭:</span><span class="sxs-lookup"><span data-stu-id="ecb3e-207">Then, you can get actionable recommendations in hello **Cost** tab in hello Advisor dashboard:</span></span>

![Advisor cost 권장 지침 예제 스크린 샷](./media/billing-getting-started/advisor-action.PNG)

<span data-ttu-id="ecb3e-209">자세한 내용은 [Advisor 비용 권장 사항](../advisor/advisor-cost-recommendations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-209">For more information, see [Advisor Cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

### <span data-ttu-id="ecb3e-210"><a name="invoice-and-usage"></a> 첫 번째 청구 기간 후 청구서 및 세부 사용 현황 받기</span><span class="sxs-lookup"><span data-stu-id="ecb3e-210"><a name="invoice-and-usage"></a> Get your invoice and detail usage after your first billing period</span></span>

<span data-ttu-id="ecb3e-211">첫 번째 청구 기간이 지난 후 Portable Document Format(.pdf) 송장 및 쉼표로 구분된 값(.csv) 사용 현황 세부 정보를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-211">After your first billing period, you can download your Portable Document Format (.pdf) invoice and Comma-Separated Values (.csv) usage details.</span></span> <span data-ttu-id="ecb3e-212">또한에 선택할 수 있습니다 toohave 청구서 tooyou 전자 메일로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-212">You can also opt in toohave your invoice emailed tooyou.</span></span> <span data-ttu-id="ecb3e-213">이러한 파일 궁극적으로 청구 tooyou 세금, 할인 및 크레딧 후 이란 toounderstand 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-213">These files help toounderstand what is ultimately billed tooyou after tax, discounts, and credits.</span></span> <span data-ttu-id="ecb3e-214">지불 연결 된 메서드 tooyour 구독을 보유 하지 않은 이러한 파일을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-214">If you didn't have a payment method attached tooyour subscription, these files might be unavailable for you.</span></span> <span data-ttu-id="ecb3e-215">자세한 내용은 참조 [어떻게 tooget 프로그램 Azure 청구 청구서 및 일일 사용량 데이터](billing-download-azure-invoice-daily-usage-date.md) 및 [Microsoft azure 청구서 이해](billing-understand-your-bill.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-215">For more information, see [How tooget your Azure billing invoice and daily usage data](billing-download-azure-invoice-daily-usage-date.md) and [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span>

![.pdf 송장 스크린 샷](./media/billing-getting-started/invoice.png)

<span data-ttu-id="ecb3e-217">이전에 설정 하는 hello 태그가 hello 세부 사용 현황.csv 파일에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-217">hello tags that you set earlier show up in hello detail usage .csv files:</span></span>

![Hello 사용.csv에 태그를 보여 주는 스크린샷](./media/billing-getting-started/csv.png)

### <a name="billing-api"></a><span data-ttu-id="ecb3e-219">청구 API</span><span class="sxs-lookup"><span data-stu-id="ecb3e-219">Billing API</span></span>

<span data-ttu-id="ecb3e-220">청구 API tooprogrammatically get 사용 현황 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-220">Use our billing API tooprogrammatically get usage data.</span></span> <span data-ttu-id="ecb3e-221">Hello RateCard API 및 hello 사용량 API 함께 tooget 청구 사용량을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-221">Use hello RateCard API and hello Usage API together tooget your billed usage.</span></span> <span data-ttu-id="ecb3e-222">자세한 내용은 [Microsoft Azure 리소스 소비에 대한 통찰력 얻기](billing-usage-rate-card-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-222">For more information, see [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md).</span></span>

## <span data-ttu-id="ecb3e-223"><a name="other-offers"></a> EA, CSP 및 스폰서쉽에 대한 추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ecb3e-223"><a name="other-offers"></a> Additional resources for EA, CSP, and Sponsorship</span></span>

<span data-ttu-id="ecb3e-224">Tooyour 계정 관리자 또는 Azure 파트너 tooget 시작에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-224">Talk tooyour account manager or Azure partner tooget started.</span></span>

| <span data-ttu-id="ecb3e-225">제안</span><span class="sxs-lookup"><span data-stu-id="ecb3e-225">Offer</span></span> | <span data-ttu-id="ecb3e-226">리소스</span><span class="sxs-lookup"><span data-stu-id="ecb3e-226">Resources</span></span> |
|-------------------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="ecb3e-227">EA(기업 계약)</span><span class="sxs-lookup"><span data-stu-id="ecb3e-227">Enterprise Agreement (EA)</span></span> | <span data-ttu-id="ecb3e-228">[EA 포털](https://ea.azure.com/), [도움말 문서](https://ea.azure.com/helpdocs) 및 [Power BI 보고서](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/)</span><span class="sxs-lookup"><span data-stu-id="ecb3e-228">[EA portal](https://ea.azure.com/), [help docs](https://ea.azure.com/helpdocs), and [Power BI report](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/)</span></span> |
| <span data-ttu-id="ecb3e-229">CSP(클라우드 솔루션 공급자)</span><span class="sxs-lookup"><span data-stu-id="ecb3e-229">Cloud Solution Provider (CSP)</span></span> | <span data-ttu-id="ecb3e-230">Tooyour 공급자와 통신</span><span class="sxs-lookup"><span data-stu-id="ecb3e-230">Talk tooyour provider</span></span> |
| <span data-ttu-id="ecb3e-231">Azure 스폰서쉽</span><span class="sxs-lookup"><span data-stu-id="ecb3e-231">Azure Sponsorship</span></span> | [<span data-ttu-id="ecb3e-232">스폰서쉽 포털</span><span class="sxs-lookup"><span data-stu-id="ecb3e-232">Sponsorship portal</span></span>](https://www.microsoftazuresponsorships.com/) |

<span data-ttu-id="ecb3e-233">관리 하는 경우 IT 읽기 대규모 조직에 대 한 권장 [Azure enterprise 스 캐 폴드](../azure-resource-manager/resource-manager-subscription-governance.md) 및 hello [엔터프라이즈 IT 백서](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf 다운로드를 영어로 제공).</span><span class="sxs-lookup"><span data-stu-id="ecb3e-233">If you're managing IT for a large organization, we recommend reading [Azure enterprise scaffold](../azure-resource-manager/resource-manager-subscription-governance.md) and hello [enterprise IT white paper](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf download, English only).</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="ecb3e-234">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="ecb3e-234">Need help?</span></span> <span data-ttu-id="ecb3e-235">지원에 문의</span><span class="sxs-lookup"><span data-stu-id="ecb3e-235">Contact support</span></span>

<span data-ttu-id="ecb3e-236">도움이 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb3e-236">If you need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>

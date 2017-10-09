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
ms.openlocfilehash: d380f27861531351ac8e570469c59a84b9ca99e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-charges-with-azure-billing-and-cost-management"></a><span data-ttu-id="0eb91-104">Azure 청구 및 비용 관리를 사용하여 예기치 않은 비용 방지</span><span class="sxs-lookup"><span data-stu-id="0eb91-104">Prevent unexpected charges with Azure billing and cost management</span></span>

<span data-ttu-id="0eb91-105">Azure에 등록할 때 몇 가지 방법으로 사용자 지출 잘 알 tooget를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-105">When you sign up for Azure, there are several things you can do tooget a better idea of your spend.</span></span> <span data-ttu-id="0eb91-106">hello [가격 계산기](https://azure.microsoft.com/pricing/calculator/) Azure 리소스를 만들기 전에 비용의 추정치를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-106">hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/) can provide an estimate of costs before you create an Azure resource.</span></span> <span data-ttu-id="0eb91-107">hello [Azure 포털](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) 구독에 대 한 hello 현재 비용 분석 및 예측을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-107">hello [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) provides you with hello current cost breakdown and forecast for your subscription.</span></span> <span data-ttu-id="0eb91-108">원하는 toogroup 하 고 다른 프로젝트 또는 팀에 대 한 비용을 이해 하는 경우 확인 [리소스 태그 지정](../azure-resource-manager/resource-group-using-tags.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-108">If you want toogroup and understand costs for different projects or teams, look at [resource tagging](../azure-resource-manager/resource-group-using-tags.md).</span></span> <span data-ttu-id="0eb91-109">조직에 toouse 선호 하는 보고 시스템을 체크 아웃 hello [Api 청구](billing-usage-rate-card-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-109">If your organization has a reporting system that you prefer toouse, check out hello [billing APIs](billing-usage-rate-card-overview.md).</span></span> 

<span data-ttu-id="0eb91-110">수도 있습니다 [송장 지난 다운로드 및 사용 현황 파일에 자세히 설명](billing-download-azure-invoice-daily-usage-date.md) toomake 올바르게 요금이 부과 되었는지 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-110">You can also [download past invoices and detail usage files](billing-download-azure-invoice-daily-usage-date.md) toomake sure you were charged correctly.</span></span> <span data-ttu-id="0eb91-111">청구서에서 일간 사용 현황 비교에 대한 자세한 내용은 [Microsoft Azure 청구서 이해](billing-understand-your-bill.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eb91-111">For more information about comparing your daily usage with your invoice, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span>

<span data-ttu-id="0eb91-112">EA (기업 계약), 클라우드 솔루션 공급자 (CSP) 또는 Azure 스폰서쉽을 통해 구독이 있는 경우이 문서에 많은 기능 tooyou를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-112">If your subscription is through an Enterprise Agreement (EA), Cloud Solution Provider (CSP), or Azure Sponsorship, then many features in this article don't apply tooyou.</span></span> <span data-ttu-id="0eb91-113">대신 비용 관리에 사용할 수 있는 다른 도구 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-113">Instead, we have a different set of tools that you can use for cost management.</span></span> <span data-ttu-id="0eb91-114">See [EA, CSP 및 스폰서쉽에 대한 추가 리소스](#other-offers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eb91-114">See [Additional resources for EA, CSP, and Sponsorship](#other-offers).</span></span>

<span data-ttu-id="0eb91-115">구독이 평가판, [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), AIO(Azure in Open) 또는 BizSpark인 경우 크레딧을 다 사용한 경우 구독이 자동으로 사용되지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-115">If your subscription is a Free Trial, [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure in Open (AIO), or BizSpark, your subscription will be automatically disabled when all your credits are used.</span></span> <span data-ttu-id="0eb91-116">에 대 한 자세한 내용은 [지출 한도](#spending-limit) tooavoid unexpectantly 사용 하지 않도록 설정 하 여 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-116">Learn about [spending limits](#spending-limit) tooavoid having your subscription unexpectantly disabled.</span></span> 

## <a name="get-estimated-costs-before-adding-azure-services"></a><span data-ttu-id="0eb91-117">Azure 서비스를 추가하기 전에 예상 비용 얻기</span><span class="sxs-lookup"><span data-stu-id="0eb91-117">Get estimated costs before adding Azure services</span></span>

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a><span data-ttu-id="0eb91-118">예상 비용 온라인 hello 가격 계산기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0eb91-118">Estimate cost online using hello pricing calculator</span></span>

<span data-ttu-id="0eb91-119">체크 아웃 hello [가격 계산기](https://azure.microsoft.com/pricing/calculator/) tooget에 관심이 hello 서비스의 월별 예상된 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-119">Check out hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/) tooget an estimated monthly cost of hello service you're interested in.</span></span> <span data-ttu-id="0eb91-120">모든 첫 번째 파티 Azure 리소스 tooget 예상 비용을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-120">You can add any first party Azure resource tooget an estimate cost.</span></span>

![Hello 가격 계산기 메뉴의 스크린 샷](./media/billing-getting-started/pricing-calc.png)

<span data-ttu-id="0eb91-122">예를 들어 A1 Windows 가상 컴퓨터 (VM)은 예상된 toocost hello 전체 시간에 실행 파일을 그대로 둘 경우 $66.96 USD/월에 시간 계산입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-122">For example, an A1 Windows Virtual Machine (VM) is estimated toocost $66.96 USD/month in compute hours if you leave it running hello whole time:</span></span>

![Hello 가격 계산기 A1 Windows VM 매달 예상된 toocost $66.96 USD 임을 보여 주는 스크린샷](./media/billing-getting-started/pricing-calcVM.png)

<span data-ttu-id="0eb91-124">가격 책정에 대한 자세한 내용은 이 [FAQ](https://azure.microsoft.com/pricing/faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eb91-124">For more information on pricing, see this [FAQ](https://azure.microsoft.com/pricing/faq/).</span></span> <span data-ttu-id="0eb91-125">또는 tootalk tooan Azure 영업 직원을 하려는 경우 1-800-867-1389에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0eb91-125">Or if you want tootalk tooan Azure salesperson, contact 1-800-867-1389.</span></span>

### <a name="review-hello-estimated-cost-in-hello-azure-portal"></a><span data-ttu-id="0eb91-126">검토 hello 예상 비용 hello Azure 포털에서</span><span class="sxs-lookup"><span data-stu-id="0eb91-126">Review hello estimated cost in hello Azure portal</span></span>

<span data-ttu-id="0eb91-127">일반적으로 hello Azure 포털에서에서 서비스를 추가 하면 매달 유사한 예상된 비용을 표시 하는 보기는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-127">Typically when you add a service in hello Azure portal, there's a view that shows you a similar estimated cost per month.</span></span> <span data-ttu-id="0eb91-128">예를 들어 Windows VM의 hello 크기를 선택 하면 hello hello 계산 시간에 대 한 월별 비용을 예상 표시:</span><span class="sxs-lookup"><span data-stu-id="0eb91-128">For example, when you choose hello size of your Windows VM, you see hello estimated monthly cost for hello compute hours:</span></span>

![예: A1 Windows VM은 매달 예상된 toocost $66.96 USD](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="set-up-billing-alerts"></a><span data-ttu-id="0eb91-130">청구 경고 설정</span><span class="sxs-lookup"><span data-stu-id="0eb91-130">Set up billing alerts</span></span>

<span data-ttu-id="0eb91-131">청구 경고 설정 tooget 전자 메일 사용 비용 지정 하는 금액을 초과 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="0eb91-131">Set up billing alerts tooget emails when your usage costs exceed an amount that you specify.</span></span> <span data-ttu-id="0eb91-132">월별 크레딧이 있는 경우 지정된 금액을 다 사용하는 경우에 대해 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-132">If you have monthly credits, set up alerts for when you use up a specified amount.</span></span> <span data-ttu-id="0eb91-133">자세한 내용은 [Microsoft Azure 구독에 대한 청구 경고 설정](billing-set-up-alerts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eb91-133">For more information, see [Set up billing alerts for your Microsoft Azure subscriptions](billing-set-up-alerts.md).</span></span>

![청구 경고 전자 메일 스크린 샷](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> <span data-ttu-id="0eb91-135">이 기능은 미리 보기 상태이므로 정기적으로 사용 현황을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-135">This feature is still in preview so you should check your usage regularly.</span></span>

<span data-ttu-id="0eb91-136">Toouse hello hello 첫 번째 경고에 대 한 지침으로 가격 계산기에서에서 예상 비용을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-136">You might want toouse hello cost estimate from hello pricing calculator as a guideline for your first alert.</span></span>

### <span data-ttu-id="0eb91-137"><a name="spending-limit"></a> 지출 한도가 설정되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="0eb91-137"><a name="spending-limit"></a> Check if you have a spending limit on</span></span>

<span data-ttu-id="0eb91-138">크레딧을 사용 하는 구독을 사용 하는 경우 다음 hello 지출 한도 대해 켜져 있습니다 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-138">If you have a subscription that uses credits, then hello spending limit is turned on for you by default.</span></span> <span data-ttu-id="0eb91-139">이러한 방식으로 모든 크레딧을 지출하면 신용 카드에 요금이 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-139">This way, when you spend all your credits, your credit card doesn't get charged.</span></span> <span data-ttu-id="0eb91-140">Hello 참조 [전체 목록은 Azure 혜택 및 지출 한도의 가용성을 hello](https://azure.microsoft.com/support/legal/offer-details/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-140">See hello [full list of Azure offers and hello availability of spending limit](https://azure.microsoft.com/support/legal/offer-details/).</span></span>

<span data-ttu-id="0eb91-141">그러나 지출 한도에 도달하면 서비스는 사용되지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-141">However, if you hit your spending limit, your services get disabled.</span></span> <span data-ttu-id="0eb91-142">즉, VM이 할당 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-142">That means your VMs are deallocated.</span></span> <span data-ttu-id="0eb91-143">tooavoid 서비스 가동 중지 시간이 꺼야 hello 지출 한도입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-143">tooavoid service downtime, you must turn off hello spending limit.</span></span> <span data-ttu-id="0eb91-144">초과분이 파일의 신용 카드에 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-144">Any overage gets charged onto your credit card on file.</span></span> 

<span data-ttu-id="0eb91-145">하 한 (를) 가져왔습니다 지출 한도를 경우 toosee 이동 toohello [구독 보기는 hello r e 계정 센터에서에서](https://account.windowsazure.com/Subscriptions)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-145">toosee if you've got spending limit on, go toohello [Subscriptions view in hello Account Center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="0eb91-146">지출 한도가 켜져 있으면 배너가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-146">A banner appears if your spending limit is on:</span></span>

![지출 한도 hello r e 계정 센터에 있는 것에 대 한 경고를 보여 주는 스크린샷](./media/billing-getting-started/spending-limit-banner.PNG)

<span data-ttu-id="0eb91-148">Hello 배너를 클릭 하 고 프롬프트 tooremove hello 지출 한도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-148">Click hello banner and follow prompts tooremove hello spending limit.</span></span> <span data-ttu-id="0eb91-149">등록할 때 신용 카드 정보를 입력 하지 않은 tooremove hello 지출 한도 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-149">If you didn't enter credit card information when you signed up, you must enter it tooremove hello spending limit.</span></span> <span data-ttu-id="0eb91-150">자세한 내용은 참조 [Azure 지출 한도-작동 방식과 tooenable 제거](https://azure.microsoft.com/pricing/spending-limits/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-150">For more information, see [Azure spending limit – How it works and how tooenable or remove it](https://azure.microsoft.com/pricing/spending-limits/).</span></span>

## <a name="ways-toomonitor-your-costs-when-using-azure-services"></a><span data-ttu-id="0eb91-151">같은 방법으로 toomonitor Azure 서비스를 사용 하는 경우 비용</span><span class="sxs-lookup"><span data-stu-id="0eb91-151">Ways toomonitor your costs when using Azure services</span></span>

### <span data-ttu-id="0eb91-152"><a name="tags"></a>태그 tooyour 리소스 toogroup 청구 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="0eb91-152"><a name="tags"></a> Add tags tooyour resources toogroup your billing data</span></span>

<span data-ttu-id="0eb91-153">지원 되는 서비스에 대 한 태그 toogroup 청구 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-153">You can use tags toogroup billing data for supported services.</span></span> <span data-ttu-id="0eb91-154">예를 들어 서로 다른 팀에 대 한 여러 Vm을 실행 하는 경우 태그 toocategorize 비용 비용 센터 (마케팅, 재무 HR) 또는 (프로덕션, 사전 프로덕션 테스트) 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-154">For example, if you run several VMs for different teams, then you can use tags toocategorize costs by cost center (HR, marketing, finance) or environment (production, pre-production, test).</span></span> 

![Hello 포털에 태그를 설정을 보여 주는 스크린샷](./media/billing-getting-started/tags.PNG)

<span data-ttu-id="0eb91-156">hello 태그가 서로 다른 비용이 보고 보기에서 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-156">hello tags show up throughout different cost reporting views.</span></span> <span data-ttu-id="0eb91-157">예를 들어 지금 바로 [비용 분석 보기](#costs)에 표시되거나 첫 번째 청구 기간 후에 [상세 사용 현황 .csv](#invoice-and-usage)에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-157">For example, they're visible in your [cost analysis view](#costs) right away and [detail usage .csv](#invoice-and-usage) after your first billing period.</span></span>

<span data-ttu-id="0eb91-158">자세한 내용은 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](../azure-resource-manager/resource-group-using-tags.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-158">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>

### <span data-ttu-id="0eb91-159"><a name="costs"></a>정기적으로 hello 비용 분석 포털에서 확인 및 진행 속도</span><span class="sxs-lookup"><span data-stu-id="0eb91-159"><a name="costs"></a> Regularly check hello portal for cost breakdown and burn rate</span></span>

<span data-ttu-id="0eb91-160">서비스가 실행 중일 때 부과되는 요금을 정기적으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-160">After you get your services running, regularly check how much they're costing you.</span></span> <span data-ttu-id="0eb91-161">Hello 현재 볼 수 있습니다 지출 및 Azure 포털에서 진행 되는 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-161">You can see hello current spend and burn rate in Azure portal.</span></span> 

1. <span data-ttu-id="0eb91-162">Hello 방문 [Azure 포털에서 구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) 하 고 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-162">Visit hello [Subscriptions blade in Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) and select a subscription.</span></span>

2. <span data-ttu-id="0eb91-163">Hello 비용 분석 결과 볼 하 고 hello 팝업 블레이드에서 진행 속도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-163">You should see hello cost breakdown and burn rate in hello popup blade.</span></span> <span data-ttu-id="0eb91-164">(Hello 맨 위 근처에 경고가 표시는) 자신의 구독에 지원 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-164">It may not be supported for your offer (a warning would be displayed near hello top).</span></span>

    ![진행 속도 및 hello Azure 포털에서에서 분할의 스크린 샷](./media/billing-getting-started/burn-rate.PNG)

3. <span data-ttu-id="0eb91-166">클릭 **비용 분석** hello 목록 toohello 왼쪽된 toosee hello 비용 별로 분석 리소스에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-166">Click **Cost analysis** in hello list toohello left toosee hello cost breakdown by resource.</span></span> <span data-ttu-id="0eb91-167">데이터 toopopulate hello에 대 한 서비스를 추가한 후 24 시간 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-167">Wait 24 hours after you add a service for hello data toopopulate.</span></span>

    ![Azure 포털에서 hello 비용 분석 보기의 스크린샷](./media/billing-getting-started/cost-analysis.PNG)

4. <span data-ttu-id="0eb91-169">[태그](#tags), 리소스 그룹 및 시간 간격 등의 다양한 속성별로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-169">You can filter by different properties like [tags](#tags), resource group, and timespan.</span></span> <span data-ttu-id="0eb91-170">클릭 **적용** tooconfirm hello 필터 및 **다운로드** tooexport hello tooa 쉼표로 구분 된 값 (.csv) 파일 보기에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-170">Click **Apply** tooconfirm hello filters and **Download** if you want tooexport hello view tooa Comma-Separated Values (.csv) file.</span></span>

5. <span data-ttu-id="0eb91-171">또한 리소스를 눌러도 toosee 지출 기록과 얼마나 hello 리소스 비용이 매일 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-171">Additionally, you can click a resource toosee spend history and how much hello resource costs each day.</span></span>

    ![Hello 스크린샷 지출 Azure 포털에서 기록 보기](./media/billing-getting-started/costhistory.PNG)

<span data-ttu-id="0eb91-173">Hello 비용 hello 예상치 hello 서비스 선택한 때 참조를 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-173">We recommend that you check hello costs you see with hello estimates you saw when you selected hello services.</span></span> <span data-ttu-id="0eb91-174">Hello 비용 예측에서 크게 다른 경우 리소스에 대해 선택한 계획 (A1 vs A0 VM 예를 들어) 가격 hello를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-174">If hello costs wildly differ from estimates, double check hello pricing plan (A1 vs A0 VM, for example) that you've selected for your resources.</span></span> 

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a><span data-ttu-id="0eb91-175">VM에 대한 자동 종료와 같은 비용 절감에 기능 사용 고려</span><span class="sxs-lookup"><span data-stu-id="0eb91-175">Consider enabling cost-cutting features like auto-shutdown for VMs</span></span>

<span data-ttu-id="0eb91-176">시나리오에 따라 hello Azure 포털에서에서 Vm에 대 한 자동 종료를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-176">Depending on your scenario, you could configure auto-shutdown for your VMs in hello Azure portal.</span></span> <span data-ttu-id="0eb91-177">자세한 내용은 [Azure Resource Manager를 사용한 VM에 대한 자동 종료](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eb91-177">For more information, see [Auto-shutdown for VMs using Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).</span></span>

![Hello 포털에서 자동 종료 옵션의 스크린 샷](./media/billing-getting-started/auto-shutdown.PNG)

<span data-ttu-id="0eb91-179">자동 종료 내에서 종료 하면 VM 전원 옵션으로 hello와 같을 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-179">Auto-shutdown isn't hello same as when you shut down within hello VM with power options.</span></span> <span data-ttu-id="0eb91-180">자동 종료 중지 하 고 자세한 사용 요금 Vm toostop 할당을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-180">Auto-shutdown stops and deallocates your VMs toostop additional usage charges.</span></span> <span data-ttu-id="0eb91-181">자세한 내용은 VM 상태에 대한 [Linux VM](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) 및 [Windows VM](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)의 가격 책정 FAQ를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eb91-181">For more information, see pricing FAQ for [Linux VMs](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) and [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) about VM states.</span></span>

<span data-ttu-id="0eb91-182">개발 및 테스트 환경에 대한 추가 비용 절감에 기능에 대해서는 [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0eb91-182">For more cost-cutting features for your development and test environments, check out [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).</span></span>

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a><span data-ttu-id="0eb91-183">Azure Advisor 권장 지침 설정 및 확인</span><span class="sxs-lookup"><span data-stu-id="0eb91-183">Turn on and check out Azure Advisor recommendations</span></span>

<span data-ttu-id="0eb91-184">[Azure Advisor](../advisor/advisor-overview.md)는 사용량이 낮은 리소스를 식별하여 비용을 절감하는 데 도움을 주는 미리 보기 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-184">[Azure Advisor](../advisor/advisor-overview.md) is a preview feature that helps you reduce costs by identifying resources with low usage.</span></span> <span data-ttu-id="0eb91-185">켜십시오 hello Azure 포털에서:</span><span class="sxs-lookup"><span data-stu-id="0eb91-185">Turn it on in hello Azure portal:</span></span>

![Azure Portal의 Azure Advisor 단추 스크린 샷](./media/billing-getting-started/advisor-button.PNG)

<span data-ttu-id="0eb91-187">그런 다음 권장 hello에 볼 수 있습니다 **비용** hello 관리자 대시보드 탭:</span><span class="sxs-lookup"><span data-stu-id="0eb91-187">Then, you can get actionable recommendations in hello **Cost** tab in hello Advisor dashboard:</span></span>

![Advisor cost 권장 지침 예제 스크린 샷](./media/billing-getting-started/advisor-action.PNG)

<span data-ttu-id="0eb91-189">자세한 내용은 [Advisor 비용 권장 사항](../advisor/advisor-cost-recommendations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eb91-189">For more information, see [Advisor Cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

### <a name="billing-api"></a><span data-ttu-id="0eb91-190">청구 API</span><span class="sxs-lookup"><span data-stu-id="0eb91-190">Billing API</span></span>

<span data-ttu-id="0eb91-191">청구 API tooprogrammatically get 사용 현황 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-191">Use our billing API tooprogrammatically get usage data.</span></span> <span data-ttu-id="0eb91-192">Hello RateCard API 및 hello 사용량 API 함께 tooget 청구 사용량을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-192">Use hello RateCard API and hello Usage API together tooget your billed usage.</span></span> <span data-ttu-id="0eb91-193">자세한 내용은 [Microsoft Azure 리소스 소비에 대한 통찰력 얻기](billing-usage-rate-card-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eb91-193">For more information, see [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md).</span></span>

## <span data-ttu-id="0eb91-194"><a name="other-offers"></a> 추가 리소스 및 특수 사례</span><span class="sxs-lookup"><span data-stu-id="0eb91-194"><a name="other-offers"></a> Additional resources and special cases</span></span>

### <a name="ea-csp-and-sponsorship-customers"></a><span data-ttu-id="0eb91-195">EA, CSP 및 스폰서쉽 고객</span><span class="sxs-lookup"><span data-stu-id="0eb91-195">EA, CSP and Sponsorship customers</span></span>
<span data-ttu-id="0eb91-196">Tooyour 계정 관리자 또는 Azure 파트너 tooget 시작에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0eb91-196">Talk tooyour account manager or Azure partner tooget started.</span></span>

| <span data-ttu-id="0eb91-197">제안</span><span class="sxs-lookup"><span data-stu-id="0eb91-197">Offer</span></span> | <span data-ttu-id="0eb91-198">리소스</span><span class="sxs-lookup"><span data-stu-id="0eb91-198">Resources</span></span> |
|-------------------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="0eb91-199">EA(기업 계약)</span><span class="sxs-lookup"><span data-stu-id="0eb91-199">Enterprise Agreement (EA)</span></span> | <span data-ttu-id="0eb91-200">[EA 포털](https://ea.azure.com/), [도움말 문서](https://ea.azure.com/helpdocs) 및 [Power BI 보고서](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/)</span><span class="sxs-lookup"><span data-stu-id="0eb91-200">[EA portal](https://ea.azure.com/), [help docs](https://ea.azure.com/helpdocs), and [Power BI report](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/)</span></span> |
| <span data-ttu-id="0eb91-201">CSP(클라우드 솔루션 공급자)</span><span class="sxs-lookup"><span data-stu-id="0eb91-201">Cloud Solution Provider (CSP)</span></span> | <span data-ttu-id="0eb91-202">Tooyour 공급자와 통신</span><span class="sxs-lookup"><span data-stu-id="0eb91-202">Talk tooyour provider</span></span> |
| <span data-ttu-id="0eb91-203">Azure 스폰서쉽</span><span class="sxs-lookup"><span data-stu-id="0eb91-203">Azure Sponsorship</span></span> | [<span data-ttu-id="0eb91-204">스폰서쉽 포털</span><span class="sxs-lookup"><span data-stu-id="0eb91-204">Sponsorship portal</span></span>](https://www.microsoftazuresponsorships.com/) |

<span data-ttu-id="0eb91-205">관리 하는 경우 IT 읽기 대규모 조직에 대 한 권장 [Azure enterprise 스 캐 폴드](../azure-resource-manager/resource-manager-subscription-governance.md) 및 hello [엔터프라이즈 IT 백서](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf 다운로드를 영어로 제공).</span><span class="sxs-lookup"><span data-stu-id="0eb91-205">If you're managing IT for a large organization, we recommend reading [Azure enterprise scaffold](../azure-resource-manager/resource-manager-subscription-governance.md) and hello [enterprise IT white paper](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf download, English only).</span></span>

### <a name="check-your-subscription-and-access"></a><span data-ttu-id="0eb91-206">구독 및 액세스 권한 확인</span><span class="sxs-lookup"><span data-stu-id="0eb91-206">Check your subscription and access</span></span>

<span data-ttu-id="0eb91-207">보기 비용 필요 [구독 액세스 toobilling 정보](billing-manage-access.md), 계정 관리자만 hello hello에 액세스할 수 있지만 [r e 계정 센터](https://account.windowsazure.com/Home/Index), 대금 청구 정보를 변경 하 고 구독을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-207">Viewing costs require [subscriptions-level access toobilling information](billing-manage-access.md), but only hello Account admin can access hello [Account Center](https://account.windowsazure.com/Home/Index), change billing info, and manage subscriptions.</span></span> <span data-ttu-id="0eb91-208">admin 님 안녕하세요 계정은 hello 등록 프로세스 진행 hello 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-208">hello Account admin is hello person who went through hello sign-up process.</span></span> <span data-ttu-id="0eb91-209">자세한 내용은 참조 [hello 구독 또는 서비스를 관리 하는 Azure 관리자 역할을 추가 또는 변경](billing-add-change-azure-subscription-administrator.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-209">For more information, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="0eb91-210">toosee 계정 관리자 hello 하는 경우 이동 toohello [hello Azure 포털에서에서 구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) hello 목록에 액세스할 수 있는 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-210">toosee if you're hello Account admin, go toohello [Subscriptions blade in hello Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) and look at hello list of subscriptions you have access to.</span></span> <span data-ttu-id="0eb91-211">**내 역할** 아래에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-211">Look under **My Role**.</span></span> <span data-ttu-id="0eb91-212">*계정 관리자*가 표시되면 문제가 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-212">If it says *Account admin*, then you're ok.</span></span> <span data-ttu-id="0eb91-213">*소유자* 등이 표시되면 모든 권한이 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-213">If it says something else like *Owner*, then you don't have full privileges.</span></span>

![Hello hello Azure 포털에서에서 구독 보기의에서 사용자 역할의 스크린 샷](./media/billing-getting-started/sub-blade-view.PNG)

<span data-ttu-id="0eb91-215">계정 관리자 hello 하지 하는 경우 다른 사람이 아마도 제공한 통해 부분적인 액세스 권한을 [Azure Active Directory 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="0eb91-215">If you're not hello Account admin, then somebody probably gave you partial access via [Azure Active Directory Role-based Access Control](../active-directory/role-based-access-control-configure.md) (RBAC).</span></span> <span data-ttu-id="0eb91-216">toomanage 구독 및 청구 정보를 변경 [계정 admin 님 안녕하세요 찾을](billing-subscription-transfer.md#whoisaa) tooperform hello 작업을 요청 하십시오 또는 [hello 구독 tooyou 전송](billing-subscription-transfer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-216">toomanage subscriptions and change billing info, [find hello Account admin](billing-subscription-transfer.md#whoisaa) and ask them tooperform hello tasks or [transfer hello subscription tooyou](billing-subscription-transfer.md).</span></span>

<span data-ttu-id="0eb91-217">계정 관리자는 더 이상 사용자의 조직과 toomanage 요금 청구서 주소, 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-217">If your Account admin is no longer with your organization and you need toomanage billing, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> 
## <a name="need-help-contact-support"></a><span data-ttu-id="0eb91-218">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="0eb91-218">Need help?</span></span> <span data-ttu-id="0eb91-219">지원에 문의</span><span class="sxs-lookup"><span data-stu-id="0eb91-219">Contact support</span></span>

<span data-ttu-id="0eb91-220">도움이 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eb91-220">If you need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>

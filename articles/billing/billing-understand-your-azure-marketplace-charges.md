---
title: "Azure 외부 서비스 요금의 이해 | Microsoft Docs"
description: "이전에는 마켓플레이스로 알려진 외부 서비스의 요금 청구, Azure의 요금에 대해 알아봅니다."
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 11701ce0162113ef6c8e056d3a30fe1d8f702f92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="89f6f-103">Azure 외부 서비스 요금 청구의 이해</span><span class="sxs-lookup"><span data-stu-id="89f6f-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="89f6f-104">외부 서비스는 Azure Marketplace로 불렸습니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-104">External services used to be called Azure Marketplace.</span></span> <span data-ttu-id="89f6f-105">일반적으로 Azure에 대해 사용 가능한 제 3자에 의해 게시되었으나 Azure 내에 완전하게 통합된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="89f6f-106">예를 들어 ClearDB 및 SendGrid는 Azure에서 구입할 수 있지만 Microsoft에서 게시되지 않은 외부 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="89f6f-107">새 외부 서비스 또는 리소스를 프로비전하면 다음 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-107">When you provision a new external service or resource, a warning is shown:</span></span>

![마켓플레이스 구매 경고](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="89f6f-109">외부 서비스는 Microsoft가 아닌 회사에 의해 게시되지만 때때로 Microsoft 제품도 외부 서비스로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="89f6f-110">외부 서비스에 요금이 청구되는 방식</span><span class="sxs-lookup"><span data-stu-id="89f6f-110">How external services are billed</span></span>
- <span data-ttu-id="89f6f-111">외부 서비스는 별도로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-111">External services are billed separately.</span></span> <span data-ttu-id="89f6f-112">이러한 서비스는 Azure 구독 내에서 개별 주문으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="89f6f-113">각 서비스에 대한 청구 기간은 서비스를 구입할 때 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-113">The billing period for each service is set when you purchase the service.</span></span> <span data-ttu-id="89f6f-114">구매한 구독의 청구 기간과 혼동되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-114">Not to be confused with the billing period of the subscription under which you purchased it.</span></span> <span data-ttu-id="89f6f-115">또한 별도의 청구를 받으며 신용 카드는 별도로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="89f6f-116">각 외부 서비스에는 다른 청구 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-116">Each external service has a different billing model.</span></span> <span data-ttu-id="89f6f-117">일부 서비스는 종량제 방식으로 청구되는 반면 다른 서비스는 월별 기반 지불 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="89f6f-118">Azure 외부 서비스에 대한 신용 카드가 필요하며 청구서 지불로 외부 서비스를 구입할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="89f6f-119">외부 서비스에 대한 월별 무료 크레딧을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="89f6f-120">[무료 크레딧](https://azure.microsoft.com/pricing/spending-limits/)을 포함하는 Azure 구독을 사용하는 경우 외부 서비스 청구에 적용될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span></span> <span data-ttu-id="89f6f-121">신용 카드를 사용하여 외부 서비스를 구입합니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-121">Use a credit card to purchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-the-azure-portal"></a><span data-ttu-id="89f6f-122">Azure Portal에서 외부 서비스 지출 및 기록 보기</span><span class="sxs-lookup"><span data-stu-id="89f6f-122">View external service spending and history in the Azure portal</span></span>
<span data-ttu-id="89f6f-123">[Azure 포털](https://portal.azure.com/) 내에서 각 구독에 있는 외부 서비스의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="89f6f-124">계정 관리자 권한으로 [Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span></span>
2. <span data-ttu-id="89f6f-125">허브 메뉴에서 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-125">In the Hub menu, select **Subscriptions**.</span></span>
   
    ![허브 메뉴에서 구독 선택](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="89f6f-127">**구독** 블레이드에서 보려는 구독을 선택하고 **외부 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span></span>
   
    ![청구 블레이드에서 구독 선택](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="89f6f-129">각 외부 서비스 주문, 게시자 이름, 구입한 서비스 계층, 리소스를 지정한 이름 및 현재 주문 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span></span> <span data-ttu-id="89f6f-130">외부 서비스를 선택하여 과거 청구서를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-130">To see past bills, select an external service.</span></span>
   
    ![외부 서비스 선택](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="89f6f-132">여기에서 세금 분석 결과를 포함한 과거 청구 금액을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-132">From here, you can view past bill amounts including the tax breakdown.</span></span>
   
    ![외부 서비스 청구 내역 보기](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="89f6f-134">EA(기업 계약) 고객의 외부 서비스 지출 보기</span><span class="sxs-lookup"><span data-stu-id="89f6f-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="89f6f-135">EA 고객은 EA 포털에서 외부 서비스 지출을 살펴보고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-135">EA customers can see external service spending and download reports in the EA portal.</span></span> <span data-ttu-id="89f6f-136">시작 방법은 [EA 고객을 위한 Azure Marketplace](https://ea.azure.com/helpdocs/azureMarketplace) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89f6f-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="89f6f-137">외부 서비스 주문에 대한 지불 방법 관리</span><span class="sxs-lookup"><span data-stu-id="89f6f-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="89f6f-138">[계정 센터](https://account.windowsazure.com/)에서 외부 서비스 주문에 대한 결제 방법을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="89f6f-139">회사 또는 학교 계정으로 구독을 구매한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 지불 방법을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span></span>
> 
> 

1. <span data-ttu-id="89f6f-140">[계정 센터](https://account.windowsazure.com/)에 로그인하고 [**마켓플레이스** 탭으로 이동](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="89f6f-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![계정 센터에서 마켓플레이스 선택](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="89f6f-142">관리하려는 외부 서비스 선택</span><span class="sxs-lookup"><span data-stu-id="89f6f-142">Select the external service you want to manage</span></span>
   
    ![관리하려는 외부 서비스 선택](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="89f6f-144">페이지의 오른쪽에서 **지불 방법 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-144">Click **Change payment method** on the right side of the page.</span></span> <span data-ttu-id="89f6f-145">이 링크를 통해 지불 방법을 관리하는 다른 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-145">This link brings you to a different portal to manage your payment method.</span></span>
   
    ![주문 요약](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="89f6f-147">**정보 편집**을 클릭하고 지침을 따라 결제 정보를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-147">Click **Edit info** and follow instructions to update your payment information.</span></span>
   
    ![정보 편집 선택](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="89f6f-149">외부 서비스 주문 취소</span><span class="sxs-lookup"><span data-stu-id="89f6f-149">Cancel an external service order</span></span>
<span data-ttu-id="89f6f-150">외부 서비스 주문을 취소하려는 경우 [Azure Portal](https://portal.azure.com)에서 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="89f6f-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span></span>

![리소스 삭제](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="89f6f-152">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="89f6f-152">Need help?</span></span> <span data-ttu-id="89f6f-153">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="89f6f-153">Contact support.</span></span>
<span data-ttu-id="89f6f-154">다른 질문이 있는 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="89f6f-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>


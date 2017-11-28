---
title: "aaaUnderstand Azure 외부 서비스 요금에 | Microsoft Docs"
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
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="66ffd-103">Azure 외부 서비스 요금 청구의 이해</span><span class="sxs-lookup"><span data-stu-id="66ffd-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="66ffd-104">외부 서비스 toobe Azure 마켓플레이스 호출을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-104">External services used toobe called Azure Marketplace.</span></span> <span data-ttu-id="66ffd-105">일반적으로 Azure에 대해 사용 가능한 제 3자에 의해 게시되었으나 Azure 내에 완전하게 통합된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="66ffd-106">예를 들어 ClearDB 및 SendGrid는 Azure에서 구입할 수 있지만 Microsoft에서 게시되지 않은 외부 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="66ffd-107">새 외부 서비스 또는 리소스를 프로비전하면 다음 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-107">When you provision a new external service or resource, a warning is shown:</span></span>

![마켓플레이스 구매 경고](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="66ffd-109">외부 서비스는 Microsoft가 아닌 회사에 의해 게시되지만 때때로 Microsoft 제품도 외부 서비스로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="66ffd-110">외부 서비스에 요금이 청구되는 방식</span><span class="sxs-lookup"><span data-stu-id="66ffd-110">How external services are billed</span></span>
- <span data-ttu-id="66ffd-111">외부 서비스는 별도로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-111">External services are billed separately.</span></span> <span data-ttu-id="66ffd-112">이러한 서비스는 Azure 구독 내에서 개별 주문으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="66ffd-113">각 서비스에 대 한 청구 기간 hello hello 서비스를 구입 하는 경우 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-113">hello billing period for each service is set when you purchase hello service.</span></span> <span data-ttu-id="66ffd-114">하지 toobe hello 구독 구매를 청구 기간 hello와 혼동된 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-114">Not toobe confused with hello billing period of hello subscription under which you purchased it.</span></span> <span data-ttu-id="66ffd-115">또한 별도의 청구를 받으며 신용 카드는 별도로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="66ffd-116">각 외부 서비스에는 다른 청구 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-116">Each external service has a different billing model.</span></span> <span data-ttu-id="66ffd-117">일부 서비스는 종량제 방식으로 청구되는 반면 다른 서비스는 월별 기반 지불 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="66ffd-118">Azure 외부 서비스에 대한 신용 카드가 필요하며 청구서 지불로 외부 서비스를 구입할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="66ffd-119">외부 서비스에 대한 월별 무료 크레딧을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="66ffd-120">포함 하는 Azure 구독을 사용 하는 경우 [무료 크레딧을](https://azure.microsoft.com/pricing/spending-limits/), 서비스 비용을 tooexternal 적용된 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied tooexternal service bills.</span></span> <span data-ttu-id="66ffd-121">신용 카드 toopurchase 외부 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-121">Use a credit card toopurchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a><span data-ttu-id="66ffd-122">보기 외부 서비스 지출 및 hello Azure 포털에 기록</span><span class="sxs-lookup"><span data-stu-id="66ffd-122">View external service spending and history in hello Azure portal</span></span>
<span data-ttu-id="66ffd-123">Hello 내에서 각 구독에 있는 hello 외부 서비스의 목록을 볼 수 있습니다 [Azure 포털](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="66ffd-123">You can view a list of hello external services that are on each subscription within hello [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="66ffd-124">Toohello 로그인 [Azure 포털](https://portal.azure.com/) hello 계정 관리자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-124">Sign in toohello [Azure portal](https://portal.azure.com/) as hello account administrator.</span></span>
2. <span data-ttu-id="66ffd-125">Hello 허브 메뉴에서 선택 **구독**합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-125">In hello Hub menu, select **Subscriptions**.</span></span>
   
    ![Hello 허브 메뉴에서 구독을 선택 합니다.](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="66ffd-127">Hello에 **구독** 블레이드, tooview을 원하는 한 다음 선택 하면 선택 hello 구독 **외부 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-127">In hello **Subscriptions** blade, select hello subscription that you want tooview, and then select **External services**.</span></span>
   
    ![Hello 청구 블레이드에서 구독을 선택 합니다.](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="66ffd-129">각 외부 서비스 주문, hello 게시자 이름, 구입한 서비스 계층, hello 리소스 및 현재 주문 상태 hello에 지정한 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-129">You should see each of your external service orders, hello publisher name, service tier you bought, name you gave hello resource, and hello current order status.</span></span> <span data-ttu-id="66ffd-130">toosee 청구서를 지 나 외부 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-130">toosee past bills, select an external service.</span></span>
   
    ![외부 서비스 선택](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="66ffd-132">여기에서는 지난 청구 금액 hello 세금 분석 결과 포함 하 여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-132">From here, you can view past bill amounts including hello tax breakdown.</span></span>
   
    ![외부 서비스 청구 내역 보기](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="66ffd-134">EA(기업 계약) 고객의 외부 서비스 지출 보기</span><span class="sxs-lookup"><span data-stu-id="66ffd-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="66ffd-135">EA 고객 외부 서비스 지출 참조할 수 있으며 hello EA 포털에서 보고서를 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-135">EA customers can see external service spending and download reports in hello EA portal.</span></span> <span data-ttu-id="66ffd-136">참조 [EA 고객에 대 한 Azure 마켓플레이스](https://ea.azure.com/helpdocs/azureMarketplace) tooget 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) tooget started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="66ffd-137">외부 서비스 주문에 대한 지불 방법 관리</span><span class="sxs-lookup"><span data-stu-id="66ffd-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="66ffd-138">Hello에서 외부 서비스 주문에 대 한 결제 방법 업데이트 [r e 계정 센터](https://account.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-138">Update your payment methods for external service orders from hello [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="66ffd-139">회사 또는 학교 계정 사용 하 여 구독을 구매한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake tooyour 지불 방법 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake changes tooyour payment method.</span></span>
> 
> 

1. <span data-ttu-id="66ffd-140">Toohello 로그인 [r e 계정 센터](https://account.windowsazure.com/) 및 [toohello 이동 **마켓플레이스** 탭](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="66ffd-140">Sign in toohello [Account Center](https://account.windowsazure.com/) and [navigate toohello **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Hello r e 계정 센터에서 마켓플레이스를 선택 합니다.](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="66ffd-142">원하는 toomanage hello 외부 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-142">Select hello external service you want toomanage</span></span>
   
    ![원하는 toomanage hello 외부 서비스를 선택 합니다.](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="66ffd-144">클릭 **지불 방법 변경** hello hello 페이지의 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-144">Click **Change payment method** on hello right side of hello page.</span></span> <span data-ttu-id="66ffd-145">이 링크는 하면 tooa 다른 포털 toomanage 결제 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-145">This link brings you tooa different portal toomanage your payment method.</span></span>
   
    ![주문 요약](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="66ffd-147">클릭 **정보 편집** 지침 tooupdate 지불 정보를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-147">Click **Edit info** and follow instructions tooupdate your payment information.</span></span>
   
    ![정보 편집 선택](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="66ffd-149">외부 서비스 주문 취소</span><span class="sxs-lookup"><span data-stu-id="66ffd-149">Cancel an external service order</span></span>
<span data-ttu-id="66ffd-150">외부 서비스 주문 toocancel을 만들려는 경우 삭제 hello 리소스 hello에 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-150">If you want toocancel your external service order, delete hello resource in hello [Azure portal](https://portal.azure.com).</span></span>

![리소스 삭제](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="66ffd-152">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="66ffd-152">Need help?</span></span> <span data-ttu-id="66ffd-153">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="66ffd-153">Contact support.</span></span>
<span data-ttu-id="66ffd-154">여전히 문의 사항이 있으면, [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ffd-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>


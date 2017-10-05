---
title: "청구서로 Azure 구독 비용 지불 | Microsoft Docs"
description: "청구서로 Azure 구독 비용을 지불하는 방법을 설명합니다."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: genli
ms.openlocfilehash: edbeba95898a41e645b61aeaaec1fd897afadd61
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="submit-a-request-to-pay-azure-subscription-by-invoice"></a><span data-ttu-id="a1987-103">청구서로 Azure 구독 비용을 지불하기 위한 요청 제출</span><span class="sxs-lookup"><span data-stu-id="a1987-103">Submit a request to pay Azure subscription by invoice</span></span>

<span data-ttu-id="a1987-104">Azure 지원에 요청을 제출하여 Azure 구독에 대한 지불 방법을 청구서로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-104">You can change the payment method for your Azure subscription to invoice by submitting a request to Azure support.</span></span> <span data-ttu-id="a1987-105">요청이 승인되면 청구서 지불 방식으로 구독을 설정하는 방법에 대한 지침이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-105">Once your request is approved, you are provided instructions on how to set up your subscription for the invoice payment method.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="a1987-106">청구서 지불은 비즈니스 계정에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-106">Invoice pay is only available for business accounts.</span></span>
> * <span data-ttu-id="a1987-107">[타사 및 외부 서비스](billing-understand-your-azure-marketplace-charges.md)는 청구서 지불을 통해 구입하거나 결제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-107">[Third party and external services](billing-understand-your-azure-marketplace-charges.md) cannot be purchased or paid for using invoice pay.</span></span> <span data-ttu-id="a1987-108">구독에 ClearDB 또는 SendGrid와 같은 외부 서비스의 리소스가 포함되어 있으면 청구서 지불로 변경하기 전에 해당 리소스를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-108">If your subscription contains resources from external services like ClearDB or SendGrid, they need be deleted before changing to invoice pay.</span></span> <span data-ttu-id="a1987-109">청구서 지불로 전환한 후에 외부 서비스를 구입하려면 신용 카드 또는 직불 카드를 사용한 별도 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-109">To purchase external services after switching to invoice pay, you need a separate subscription with a credit or debit card.</span></span>
> * <span data-ttu-id="a1987-110">일단 청구서 지불로 전환한 경우 신용 카드 또는 직불 카드 결제로 다시 전환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-110">Once you switch to invoice pay, you can't switch back to credit or debit card payment.</span></span>

## <a name="request-pay-by-invoice"></a><span data-ttu-id="a1987-111">청구서로 지불 요청</span><span class="sxs-lookup"><span data-stu-id="a1987-111">Request pay by invoice</span></span>

1. <span data-ttu-id="a1987-112">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-112">Sign into the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="a1987-113">**도움말 + 지원** > **새 지원 요청**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-113">Select **Help + support** > **New support request**.</span></span>

    ![도움말 및 지원 단추](./media/billing-how-to-pay-by-invoice/helpandsupport.png)
1. <span data-ttu-id="a1987-115">문제 유형으로 **청구**를 선택하고 청구서로 결제할 구독을 선택한 후 지원 계획을 선택하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-115">Select **Billing** as the issue type, select the subscription for which you want to pay by invoice, select a support plan, and then select **Next**.</span></span>
1. <span data-ttu-id="a1987-116">**문제** 블레이드의 **문제 유형** 상자에서 **청구서로 지불**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-116">In the **Problem** blade, select **Pay by Invoice** in the **Problem Type** box.</span></span>
1. <span data-ttu-id="a1987-117">**세부 정보** 상자에 다음 정보를 입력하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-117">Enter the following information in the **Details** box, and then select **Next**.</span></span>

    * <span data-ttu-id="a1987-118">회사 이름</span><span class="sxs-lookup"><span data-stu-id="a1987-118">Company name</span></span>
    * <span data-ttu-id="a1987-119">청구 주소</span><span class="sxs-lookup"><span data-stu-id="a1987-119">Billing address</span></span>
    * [<span data-ttu-id="a1987-120">계정 관리자의 전자 메일 주소</span><span class="sxs-lookup"><span data-stu-id="a1987-120">Account administrator's email address</span></span>](billing-add-change-azure-subscription-administrator.md#check-the-account-administrator-of-the-subscription)

1. <span data-ttu-id="a1987-121">연락처 정보와 기본 연락 방법을 확인한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-121">Verify your contact information and preferred contact method, and then click **Create**.</span></span>

<span data-ttu-id="a1987-122">필요한 신용 수준 때문에 신용 검사를 실행해야 할 경우 신용 검사 신청서를 보내 드립니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-122">If we need to run a credit check because of the amount of credit that you need, we send you a credit check application.</span></span> <span data-ttu-id="a1987-123">신청서를 제출하면 신용 신청을 처리하는 데 5-7일 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1987-123">After you submit the application, the credit application can take 5-7 days to process.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="a1987-124">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="a1987-124">Need help?</span></span> <span data-ttu-id="a1987-125">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a1987-125">Contact support.</span></span>

<span data-ttu-id="a1987-126">다른 도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="a1987-126">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
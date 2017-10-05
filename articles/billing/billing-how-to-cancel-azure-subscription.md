---
title: "Azure 구독 취소 | Microsoft Docs"
description: "무료 평가판 구독과 같은 Azure 구독을 취소하는 방법을 설명합니다."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 3051d6b0-179f-4e3a-bda4-3fee7135eac5
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: genli
ms.openlocfilehash: c415fada30aa0b0bd9b9d1e416bc37ef30653f68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="cancel-your-subscription-for-azure"></a><span data-ttu-id="b9cad-103">Azure 구독 취소</span><span class="sxs-lookup"><span data-stu-id="b9cad-103">Cancel your subscription for Azure</span></span>

<span data-ttu-id="b9cad-104">[계정 관리자 권한](billing-subscription-transfer.md#whoisaa)으로 Azure 구독을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-104">You can cancel your Azure subscription as the [Account Administrator](billing-subscription-transfer.md#whoisaa).</span></span> <span data-ttu-id="b9cad-105">구독을 취소하면 Azure 서비스 및 리소스에 대한 액세스 권한이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-105">After you cancel the subscription, your access to Azure services and resources ends.</span></span>

<span data-ttu-id="b9cad-106">구독을 취소하기 전에 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-106">Before you cancel your subscription:</span></span>

* <span data-ttu-id="b9cad-107">데이터를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-107">Back up your data.</span></span> <span data-ttu-id="b9cad-108">예를 들어 Azure Storage 또는 SQL에 데이터를 저장하는 경우 복사본을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-108">For example, if you're storing data in Azure storage or SQL, download a copy.</span></span> <span data-ttu-id="b9cad-109">가상 컴퓨터를 사용하는 경우 해당 이미지를 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-109">If you have a virtual machine, save an image of it locally.</span></span>
* <span data-ttu-id="b9cad-110">서비스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-110">Shut down your services.</span></span> <span data-ttu-id="b9cad-111">[관리 포털의 페이지 리소스](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources)로 이동한 후 실행 중인 가상 컴퓨터, 응용 프로그램 또는 기타 서비스를 모두 **중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-111">Go to the [resources page in the management portal](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources), and **Stop** any running virtual machines, applications, or other services.</span></span>
* <span data-ttu-id="b9cad-112">데이터를 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-112">Consider migrating your data.</span></span> <span data-ttu-id="b9cad-113">[새 리소스 그룹 또는 구독으로 리소스 이동](../azure-resource-manager/resource-group-move-resources.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9cad-113">See [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="b9cad-114">유료 [Azure 지원 계획](https://azure.microsoft.com/support/plans/)을 취소해도 6개월 중 남은 기간에 대해 월별 요금이 계속 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-114">If you cancel a paid [Azure Support plan](https://azure.microsoft.com/support/plans/), you are still billed monthly for the rest of the 6-months term.</span></span>

## <a name="cancel-subscription-using-the-azure-portal"></a><span data-ttu-id="b9cad-115">Azure Portal을 사용하여 구독 취소</span><span class="sxs-lookup"><span data-stu-id="b9cad-115">Cancel subscription using the Azure portal</span></span>

1. <span data-ttu-id="b9cad-116">[구독 페이지](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-116">Select your subscription from the [Subscriptions page](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

1. <span data-ttu-id="b9cad-117">취소하려는 구독을 선택하고 **구독 취소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-117">Select the subscription that you want to cancel and click **Cancel subscription**.</span></span>

    ![취소 단추를 보여 주는 스크린샷](./media/billing-how-to-cancel-azure-subscription/cancel_ibiza.png)

1. <span data-ttu-id="b9cad-119">메시지에 따라 취소를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-119">Follow prompts and finish cancellation.</span></span>

## <a name="cancel-subscription-using-the-azure-account-center"></a><span data-ttu-id="b9cad-120">Azure 계정 센터를 사용하여 구독 취소</span><span class="sxs-lookup"><span data-stu-id="b9cad-120">Cancel subscription using the Azure Account Center</span></span>

1. <span data-ttu-id="b9cad-121">[Azure 계정 센터](https://account.windowsazure.com/subscriptions)에 계정 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-121">Sign in to the [Azure Account Center](https://account.windowsazure.com/subscriptions) as the Account Administrator.</span></span>

1. <span data-ttu-id="b9cad-122">**구독을 클릭하여 세부 정보 및 사용법**에서 취소하고자 하는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-122">Under **Click a subscription to view details and usage**, select the subscription that you want to cancel.</span></span>

    ![선택한 예제 구독을 보여 주는 스크린샷](./media/billing-how-to-cancel-azure-subscription/Selectsub.png)

1. <span data-ttu-id="b9cad-124">페이지의 오른쪽에서 **구독 취소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-124">On the right side of the page, select **Cancel Subscription**.</span></span>

    ![구독 취소 단추를 보여 주는 스크린샷](./media/billing-how-to-cancel-azure-subscription/cancelsub.png)

1. <span data-ttu-id="b9cad-126">**예, 구독을 취소합니다**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-126">Select **Yes, cancel my subscription**.</span></span>

    ![취소 대화 상자를 보여 주는 스크린샷](./media/billing-how-to-cancel-azure-subscription/cancelbox.png)

1. <span data-ttu-id="b9cad-128">그런 다음</span><span class="sxs-lookup"><span data-stu-id="b9cad-128">Click</span></span> ![확인 기호 단추](./media/billing-how-to-cancel-azure-subscription/checkbutton.png) <span data-ttu-id="b9cad-130">을 클릭하여 대화 창을 닫고 구독 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-130">to close the dialog window and return to your subscription page.</span></span>

## <a name="what-happens-after-i-cancel-my-subscription"></a><span data-ttu-id="b9cad-131">구독을 취소한 후에는 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="b9cad-131">What happens after I cancel my subscription?</span></span>

<span data-ttu-id="b9cad-132">취소하면 청구가 즉시 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-132">Once you cancel, billing is stopped immediately.</span></span> <span data-ttu-id="b9cad-133">그러나 취소가 포털에 표시되기까지 최대 10분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-133">However, it can take up to 10 minutes for the cancellation show in the portal.</span></span>

<span data-ttu-id="b9cad-134">그 후에는 서비스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-134">After that, your services are disabled.</span></span> <span data-ttu-id="b9cad-135">즉, 가상 컴퓨터의 할당이 취소되고 임시 IP 주소가 해제되며 저장소는 읽기 전용이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-135">That means your virtual machines are deallocated, temporary IP addresses are freed, and storage is read-only.</span></span>

<span data-ttu-id="b9cad-136">평가판을 사용 중이거나 크레딧을 사용할 수 있는 경우가 아니라면 마지막 청구 주기와 취소 날짜 사이 생성된 미불 사용 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-136">Unless you’re on a Free Trial or have credits available, you’re billed for any outstanding usage charges generated between your last billing cycle and the cancellation date.</span></span> <span data-ttu-id="b9cad-137">청구 주기가 끝난 경우 마지막 청구서를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-137">You get your last bill at the end of the billing cycle.</span></span>

<span data-ttu-id="b9cad-138">사용자가 구독을 취소하더라도 다시 액세스해야 하거나 마음이 바뀐 경우를 대비해서 90일 동안 기다렸다가 데이터를 영구 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-138">After you cancel your subscription, we wait 90 days before permanently deleting your data in case you need to access it or you change your mind.</span></span> <span data-ttu-id="b9cad-139">데이터 보존 요금은 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-139">We don't charge you for retaining the data.</span></span> <span data-ttu-id="b9cad-140">자세한 내용은 [Microsoft 보안 센터 - 데이터 관리 방법](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9cad-140">To learn more, see [Microsoft Trust Center - How we manage your data](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).</span></span>

## <a name="reactivate-subscription"></a><span data-ttu-id="b9cad-141">구독 다시 활성화</span><span class="sxs-lookup"><span data-stu-id="b9cad-141">Reactivate subscription</span></span>

<span data-ttu-id="b9cad-142">종량제 구독을 실수로 취소한 경우 [계정 센터에서 다시 활성화](billing-subscription-become-disable.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9cad-142">If you cancel your Pay-As-You-Go subscription accidentally, you can [reactivate it in the Accounts Center](billing-subscription-become-disable.md).</span></span>

<span data-ttu-id="b9cad-143">종량제 구독이 아닌 경우 구독을 다시 활성화하려면 취소 후 90일 이내에 지원 센터로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="b9cad-143">If your subscription is not Pay-As-You-Go, contact support within 90 days of cancellation to reactivate your subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="b9cad-144">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="b9cad-144">Need help?</span></span> <span data-ttu-id="b9cad-145">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="b9cad-145">Contact support.</span></span>

<span data-ttu-id="b9cad-146">다른 질문이 있는 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="b9cad-146">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

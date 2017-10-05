---
title: "Azure 등록 문제 해결 | Microsoft Docs"
description: "몇 가지 일반적인 Azure 설정 문제를 해결하는 방법에 대해 설명합니다."
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 647509ea36e487aca5db661adb3268e845988f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a><span data-ttu-id="02dee-103">Azure의 등록 문제 해결</span><span class="sxs-lookup"><span data-stu-id="02dee-103">Troubleshoot sign-up issues for Azure</span></span>
<span data-ttu-id="02dee-104">Azure에 등록할 수 없는 경우 이 문서에 있는 팁을 사용하여 일반적인 문제를 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="02dee-104">If you can't sign up for Azure, use the tips in this article to troubleshoot common issues.</span></span> <span data-ttu-id="02dee-105">등록 시 신용 카드 관련 문제가 발생하면 [Azure 등록 시 사용자의 직불 카드 또는 신용 카드가 거부되었습니다.](billing-credit-card-fails-during-azure-sign-up.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02dee-105">If you have an issue with your credit card during sign-up, see [your debit card or credit card is declined at Azure sign-up](billing-credit-card-fails-during-azure-sign-up.md).</span></span> <span data-ttu-id="02dee-106">Azure 계정이 있지만 로그인할 수 없는 경우 [내 Azure 구독 관리를 위해 로그인할 수 없습니다.](billing-cannot-login-subscription.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02dee-106">If you have an Azure account but can't sign in, see [I can't sign in to manage my Azure subscription](billing-cannot-login-subscription.md).</span></span>

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a><span data-ttu-id="02dee-107">진행 표시줄이 "카드로 ID 확인" 섹션에서 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-107">Progress bar hangs in "Identity verification by card" section</span></span>

<span data-ttu-id="02dee-108">카드를 통해 본인 여부 확인을 완료하려면 브라우저에서 타사 쿠키를 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-108">To complete the identity verification by card, third-party cookies must be allowed for your browser.</span></span>

![등록 중 중지된 카드로 ID 확인 섹션의 스크린샷](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

<span data-ttu-id="02dee-110">다음 단계를 사용하여 브라우저의 쿠키 설정을 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="02dee-110">Use the following steps to update your browser's cookie settings.</span></span>

1. <span data-ttu-id="02dee-111">Chrome을 사용하는 경우 **설정** > **고급 설정 표시** > **개인 정보** > **콘텐츠 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-111">If you're using Chrome, go to **Settings** > **Show advanced settings** > **Privacy** > **Content settings**.</span></span> <span data-ttu-id="02dee-112">**타사 쿠키 및 사이트 데이터 차단**을 선택 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-112">Uncheck **Block third-party cookies and site data**.</span></span>
2. <span data-ttu-id="02dee-113">Edge를 사용하는 경우 **설정** > **고급 설정 보기** > **쿠키**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-113">If you're using Edge, go to **Settings** > **View advanced settings** > **Cookies**.</span></span> <span data-ttu-id="02dee-114">**쿠키를 차단하지 않음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-114">Select **Don't block cookies**.</span></span>
3. <span data-ttu-id="02dee-115">Azure 등록 페이지를 새로 고치고 해당 문제가 해결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-115">Refresh the Azure sign-up page, and check if the problem is resolved.</span></span>
4. <span data-ttu-id="02dee-116">새로 고쳐도 문제가 해결되지 않을 경우에는 브라우저를 중단했다가 다시 시작하여 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="02dee-116">If the refresh didn't solve the issue, quit and restart your browser then try again.</span></span>

## <a name="credit-card-form-doesnt-support-my-billing-address"></a><span data-ttu-id="02dee-117">신용 카드 양식이 내 청구 주소를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-117">Credit card form doesn't support my billing address</span></span>
<span data-ttu-id="02dee-118">청구 주소는 **내 정보** 섹션에서 선택한 국가의 주소여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-118">Your billing address needs to be in the country that you selected in the **About you** section.</span></span> <span data-ttu-id="02dee-119">올바른 국가를 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-119">Make sure you select the correct country.</span></span>

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a><span data-ttu-id="02dee-120">계정 확인을 등록할 때 문자 메시지 또는 호출이 표시되지 않았습니다</span><span class="sxs-lookup"><span data-stu-id="02dee-120">No text messages or calls during sign-up account verification</span></span>
<span data-ttu-id="02dee-121">일반적으로 훨씬 더 빠르지만, 확인 코드가 배달되는 데 최대 4분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-121">While it is usually much faster, it may take up to four minutes for verification code to be delivered.</span></span> <span data-ttu-id="02dee-122">확인을 위해 입력한 전화 번호는 계정에 대한 연락처 번호로 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-122">The phone number you enter for verification isn't stored as a contact number for the account.</span></span>

<span data-ttu-id="02dee-123">다음은 몇 가지 추가 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-123">Here are some additional tips:</span></span>
* <span data-ttu-id="02dee-124">VOIP 전화 번호는 전화 인증 프로세스에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-124">A VOIP phone number can't be used for the phone verification process.</span></span>
* <span data-ttu-id="02dee-125">드롭다운 메뉴에서 선택한 국가 코드를 포함하여 입력한 전화 번호를 다시 한번 점검하십시오.</span><span class="sxs-lookup"><span data-stu-id="02dee-125">Double check the phone number you enter, including the country code you selected in the dropdown menu.</span></span>
* <span data-ttu-id="02dee-126">전화가 문자 메시지(SMS)를 수신하지 못하는 경우 **전화 걸기** 옵션을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-126">If your phone doesn't receive text messages (SMS), try the **Call me** option.</span></span>
* <span data-ttu-id="02dee-127">전화가 미국 기반 번호에서 전화 또는 SMS 메시지를 받을 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-127">Ensure that your phone can receive calls or SMS messages from a United States based number.</span></span>

<span data-ttu-id="02dee-128">문자 메시지 또는 전화를 받은 경우 수신한 코드를 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-128">When you get the text message or phone call, enter code that you receive into the text box.</span></span>

## <a name="credit-card-declined-or-not-accepted"></a><span data-ttu-id="02dee-129">신용 카드가 거부되거나 승인되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-129">Credit card declined or not accepted</span></span>
<span data-ttu-id="02dee-130">가상 카드, 선불 카드 또는 직불 카드는 Azure 구독의 지불 옵션으로 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-130">Virtual or prepaid credit or debit cards aren't accepted as payment for Azure subscriptions.</span></span> <span data-ttu-id="02dee-131">카드가 거절될만한 다른 이유를 확인하려면 [Azure 등록 시 사용자의 직불 카드 또는 신용 카드가 거부되었습니다.](billing-credit-card-fails-during-azure-sign-up.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02dee-131">To see what else may cause your card to be declined, see [your debit card or credit card is declined at Azure sign-up](billing-credit-card-fails-during-azure-sign-up.md).</span></span>

## <a name="free-trial-is-not-available"></a><span data-ttu-id="02dee-132">"무료 평가판은 제공되지 않습니다."</span><span class="sxs-lookup"><span data-stu-id="02dee-132">"Free Trial is not available"</span></span>
<span data-ttu-id="02dee-133">이전에 Azure 구독을 사용한 적이 있나요?</span><span class="sxs-lookup"><span data-stu-id="02dee-133">Have you used an Azure subscription in the past?</span></span> <span data-ttu-id="02dee-134">Azure 사용 약관은 Azure에 새로 추가된 사용자에 대해서만 무료 평가판 활성화하도록 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-134">The Azure Terms of Use agreement limits free trial activation only for a user that's new to Azure.</span></span> <span data-ttu-id="02dee-135">다른 유형의 Azure 구독이 있는 경우 무료 평가판을 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-135">If you have had any other type of Azure subscription, you can't activate a free trial.</span></span> <span data-ttu-id="02dee-136">[종량제 구독](https://azure.microsoft.com/offers/ms-azr-0003p/) 등록을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-136">Consider signing up for a [Pay-As-You-Go subscription](https://azure.microsoft.com/offers/ms-azr-0003p/).</span></span>

## <a name="i-saw-a-charge-on-my-free-trial-account"></a><span data-ttu-id="02dee-137">평가판 계정에 요금이 부과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-137">I saw a charge on my Free Trial account</span></span>
<span data-ttu-id="02dee-138">등록 후 신용 카드 계정에 소액의 확인용 금액이 표시될 수 있습니다. 이 표시는 3~5일 이내에 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-138">You may see a small verification hold on your credit card account after you sign up, which is removed within 3 to 5 days.</span></span> <span data-ttu-id="02dee-139">비용 관리가 염려되는 경우 [예상치 못한 비용 방지](https://docs.microsoft.com/azure/billing/billing-getting-started)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-139">If you are worried about managing costs, read more about [preventing unexpected costs](https://docs.microsoft.com/azure/billing/billing-getting-started).</span></span>

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a><span data-ttu-id="02dee-140">MSDN, BizSpark, BizSparkPlus 또는 MPN 같은 Azure 혜택 계획을 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-140">Can’t activate Azure benefit plan like MSDN, BizSpark, BizSparkPlus, or MPN</span></span>
<span data-ttu-id="02dee-141">올바른 로그인 자격 증명을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-141">Make sure that you're using the right sign-in credentials.</span></span> <span data-ttu-id="02dee-142">그런 다음 혜택 프로그램에서 자격이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-142">Then check the benefit program to make sure that you're eligible.</span></span> 

* <span data-ttu-id="02dee-143">MSDN</span><span class="sxs-lookup"><span data-stu-id="02dee-143">MSDN</span></span>
  * <span data-ttu-id="02dee-144">[MSDN 계정 페이지](https://msdn.microsoft.com/subscriptions/manage/default.aspx)에서 자격 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-144">Verify your eligibility status in your [MSDN account page](https://msdn.microsoft.com/subscriptions/manage/default.aspx).</span></span>
  * <span data-ttu-id="02dee-145">자신의 상태를 확인할 수 없는 경우 [MSDN 구독 고객 서비스 센터](https://msdn.microsoft.com/subscriptions/contactus.aspx)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="02dee-145">If you can't verify your status, contact the [MSDN Subscriptions Customer Service Centers](https://msdn.microsoft.com/subscriptions/contactus.aspx)</span></span>
* <span data-ttu-id="02dee-146">BizSpark</span><span class="sxs-lookup"><span data-stu-id="02dee-146">BizSpark</span></span>
  * <span data-ttu-id="02dee-147">[BizSpark 포털](https://www.microsoft.com/bizspark/default.aspx#start-two) 에 로그인하고 BizSpark 및 BizSpark Plus에 대한 자격 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-147">Sign in to the [BizSpark portal](https://www.microsoft.com/bizspark/default.aspx#start-two) and verify your eligibility status for BizSpark and BizSpark Plus.</span></span>
  * <span data-ttu-id="02dee-148">상태를 확인할 수 없는 경우 [BizSpark 포럼에서 도움을 받을](http://aka.ms/bzforums)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-148">If you can't verify your status, you can [get help at the BizSpark forums](http://aka.ms/bzforums).</span></span>
* <span data-ttu-id="02dee-149">MPN</span><span class="sxs-lookup"><span data-stu-id="02dee-149">MPN</span></span>
  * <span data-ttu-id="02dee-150">[MPN 포털](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) 에 로그인하고 자격 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-150">Sign in to the [MPN portal](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) and verify your eligibility status.</span></span> <span data-ttu-id="02dee-151">적절한 [클라우드 플랫폼 역량](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx)을 가지고 있는 경우 추가 혜택의 자격이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-151">If you have the appropriate [Cloud Platform Competencies](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), you may be eligible for additional benefits.</span></span>
  * <span data-ttu-id="02dee-152">자신의 상태를 확인할 수 없는 경우 [MPN 지원](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="02dee-152">If you can't verify your status, contact [MPN support](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).</span></span>

## <a name="cant-activate-new-azure-in-open-subscription"></a><span data-ttu-id="02dee-153">새 Azure In Open 구독을 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-153">Can’t activate new Azure In Open subscription</span></span>
<span data-ttu-id="02dee-154">Azure In Open 구독을 만들려면 하나 이상의 Azure In Open 토큰이 연결된 유효한 OSA(Online Service Activation) 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02dee-154">To create an Azure In Open subscription, you must have a valid Online Service Activation (OSA) key with at least one Azure In Open token associated to it.</span></span> <span data-ttu-id="02dee-155">OSA 키가 없는 경우 [Microsoft Pinpoint](http://pinpoint.microsoft.com/)에 나열된 Microsoft 파트너 중 한 곳에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="02dee-155">If you don't have an OSA key, contact one of Microsoft Partners listed in [Microsoft Pinpoint](http://pinpoint.microsoft.com/).</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="02dee-156">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="02dee-156">Need help?</span></span> <span data-ttu-id="02dee-157">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="02dee-157">Contact support.</span></span>
<span data-ttu-id="02dee-158">다른 도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="02dee-158">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

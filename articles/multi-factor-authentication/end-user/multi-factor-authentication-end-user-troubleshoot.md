---
title: "2단계 인증 문제 해결 | Microsoft Docs"
description: "이 문서는 Azure 다단계 인증에 문제가 있는 경우 수행할 작업에 대한 정보를 제공합니다."
services: multi-factor-authentication
keywords: "다단계 인증 클라이언트, 인증 문제, 상관관계 ID"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 8f3aef42-7f66-4656-a7cd-d25a971cb9eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: end-user
ms.openlocfilehash: e4b59efd12a64f58634b66590cf6999cc9e68eb6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-help-with-two-step-verification"></a><span data-ttu-id="344b4-104">2단계 인증에 관한 도움말 얻기</span><span class="sxs-lookup"><span data-stu-id="344b4-104">Get help with two-step verification</span></span>
<span data-ttu-id="344b4-105">이 문서는 2단계 인증과 관련하여 가장 많이 하는 질문에 대한 답변입니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-105">This article answers the most common questions that people ask about two-step verification.</span></span> 

## <a name="why-do-i-have-to-perform-two-step-verification-can-i-turn-it-off"></a><span data-ttu-id="344b4-106">2단계 인증을 수행해야 하는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="344b4-106">Why do I have to perform two-step verification?</span></span> <span data-ttu-id="344b4-107">이 기능을 끌 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="344b4-107">Can I turn it off?</span></span>

<span data-ttu-id="344b4-108">2단계 인증은 조직이 계정을 보호하는 데 사용하도록 선택한 보안 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-108">Two-step verification is a security feature that your organization chose to use to protect your accounts.</span></span> <span data-ttu-id="344b4-109">사용자가 알고 있는 것과 휴대하는 것, 두 가지 형태의 인증을 사용하기 때문에 단순 암호에 비해 더 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-109">It's more secure than just a password, because it relies on two forms of authentication: something you know, and something you have with you.</span></span> <span data-ttu-id="344b4-110">사용자가 알고 있는 것은 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-110">The something you know is your password.</span></span> <span data-ttu-id="344b4-111">사용자가 휴대하는 것은 사용자가 흔히 휴대하는 전화 또는 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-111">The something you have with you is a phone or device that you commonly have with you.</span></span> <span data-ttu-id="344b4-112">계정이 2단계 인증으로 보호되면 악의적인 해커가 어떻게 해서 사용자의 암호를 알아냈다 하더라도 사용자의 전화에는 접근할 수 없으므로 사용자로 로그인할 수 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-112">When your account is protected with two-step verification, that means that a malicious hacker can't sign in as you if they get your password somehow because they don't have access to your phone, too.</span></span> 

<span data-ttu-id="344b4-113">2단계 인증을 제공하는 것은 Microsoft이지만, 기능을 사용하도록 선택하는 것은 사용자의 조직입니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-113">Microsoft offers two-step verification, but your organization chooses to use the feature.</span></span> <span data-ttu-id="344b4-114">계정을 보호하기 위한 암호 사용을 거부할 수 없는 것처럼 IT 부서에서 요구하는 경우 사용자는 이를 거부할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-114">You can't opt out if your IT department requires it of you, just like you can't opt out of using a password to protect your account.</span></span> 

<span data-ttu-id="344b4-115">개인 Microsoft 계정에서 2단계 인증이 켜져 있고 설정을 변경하려는 경우 [2단계 인증 정보](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)를 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="344b4-115">If you have two-step verification turned on for your personal Microsoft account and want to change your settings, read [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) instead.</span></span> 

## <a name="i-dont-have-my-phone-with-me-today"></a><span data-ttu-id="344b4-116">현재 전화기가 없는 경우</span><span class="sxs-lookup"><span data-stu-id="344b4-116">I don't have my phone with me today</span></span>

<span data-ttu-id="344b4-117">전화기를 집에 두고 온 날에도, 직장에서는 여전히 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-117">Some days you leave your phone at home, but still need to sign in at work.</span></span> <span data-ttu-id="344b4-118">우선 다른 인증 방법으로 로그인을 시도해 보아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-118">The first thing you should try is signing in with a different verification method.</span></span> <span data-ttu-id="344b4-119">2단계 인증을 등록할 때 전화번호를 2개 이상 설정하였습니까?</span><span class="sxs-lookup"><span data-stu-id="344b4-119">When you registered for two-step verification, did you set up more than one phone number?</span></span> <span data-ttu-id="344b4-120">다른 방법으로 로그인을 시도해 보려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-120">To try signing in with a different method, follow these steps:</span></span>

1. <span data-ttu-id="344b4-121">일반적인 방법으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-121">Sign in as you normally would.</span></span>
2. <span data-ttu-id="344b4-122">2단계 인증 페이지를 열 때 **다른 인증 옵션 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-122">When the two-step verification page opens, choose **Use a different verification option**.</span></span>

   ![다양한 확인](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. <span data-ttu-id="344b4-124">사용할 인증 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-124">Select the verification option you want to use.</span></span>
4. <span data-ttu-id="344b4-125">2단계 인증을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-125">Continue with two-step verification.</span></span>

<span data-ttu-id="344b4-126">**다른 인증 옵션 사용** 링크가 표시되지 않는 경우는 처음 2단계 인증에 등록할 때 대체 방법을 설정하지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-126">If you don't see the **Use a different verification option** link, then that means you didn't set up alternative methods when you first registered for two-step verification.</span></span> <span data-ttu-id="344b4-127">계정에 로그인하는 데 관한 도움말을 보려면 IT 부서에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="344b4-127">Contact your IT department to get help signing in to your account.</span></span> <span data-ttu-id="344b4-128">로그인하고 나면, 다음 번을 위해 추가 인증 방법을 추가하도록 [설정을 관리](multi-factor-authentication-end-user-manage-settings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-128">Once you're signed in, make sure to [manage your settings](multi-factor-authentication-end-user-manage-settings.md) to add additional verification methods for next time.</span></span> 

<span data-ttu-id="344b4-129">**다른 인증 옵션 사용** 링크가 표시되지만 대체 방법에 대한 액세스 권한이 없는 경우 IT 부서에 문의하여 계정에 로그인하는 데 관한 도움을 받으세요.</span><span class="sxs-lookup"><span data-stu-id="344b4-129">If you do see the **Use a different verification option** link, but you don't have access to your alternative methods either, contact your IT department to get help signing in to your account.</span></span> 

## <a name="i-lost-my-phone-or-got-a-new-number"></a><span data-ttu-id="344b4-130">내 전화기를 분실한 경우 또는 번호가 바뀐 경우</span><span class="sxs-lookup"><span data-stu-id="344b4-130">I lost my phone or got a new number</span></span>
<span data-ttu-id="344b4-131">두 가지 방법으로 계정에 다시 들어올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-131">There are two ways to get back in to your account.</span></span> <span data-ttu-id="344b4-132">첫 번째 방법은 대체 인증 전화 번호를 설정한 경우 이를 사용하여 로그인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-132">The first is to sign in using your alternate authentication phone number, if you have set one up.</span></span> <span data-ttu-id="344b4-133">두 번째 방법은 사용자 설정을 지우도록 IT 부서에 요청하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-133">The second is to ask your IT department to clear your settings.</span></span>

<span data-ttu-id="344b4-134">전화기를 분실했거나 도난당한 경우 앱 암호를 다시 설정하고 기억된 장치를 삭제하도록 IT 부서에 알리는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-134">If your phone was lost or stolen, we also recommend that you tell your IT department so they can reset your app passwords and clear any remembered devices.</span></span> 

### <a name="use-an-alternate-phone-number"></a><span data-ttu-id="344b4-135">대체 전화 번호 사용</span><span class="sxs-lookup"><span data-stu-id="344b4-135">Use an alternate phone number</span></span>
<span data-ttu-id="344b4-136">다른 장치에서 보조 전화 번호 또는 인증자 앱을 비롯한 여러 인증 옵션을 설정한 경우 다음 중 하나를 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-136">If you have set up multiple verification options, including a secondary phone number or an authenticator app on a different device, you can use one of them to sign in.</span></span>

<span data-ttu-id="344b4-137">대체 전화 번호를 사용하여 로그인하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="344b4-137">To sign in using the alternate phone number, follow these steps:</span></span>

1. <span data-ttu-id="344b4-138">일반적인 방법으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-138">Sign in as you normally would.</span></span>
2. <span data-ttu-id="344b4-139">추가로 계정을 확인하라는 메시지가 표시되면 **다른 인증 옵션 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-139">When prompted to further verify your account, choose **Use a different verification option**.</span></span>
   
   ![다양한 확인](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. <span data-ttu-id="344b4-141">액세스 권한이 있는 전화 번호 또는 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-141">Select the phone number or device that you have access to.</span></span>
4. <span data-ttu-id="344b4-142">계정으로 다시 돌아오면 [설정을 관리](multi-factor-authentication-end-user-manage-settings.md)하여 인증 전화 번호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-142">After you're back in your account, [manage your settings](multi-factor-authentication-end-user-manage-settings.md) to change your authentication phone number.</span></span>

### <a name="clear-your-settings"></a><span data-ttu-id="344b4-143">설정 지우기</span><span class="sxs-lookup"><span data-stu-id="344b4-143">Clear your settings</span></span>
<span data-ttu-id="344b4-144">보조 인증 전화 번호를 구성하지 않은 경우 도움을 받을 수 있도록 IT 부서에게 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-144">If you have not configured a secondary authentication phone number, you have to contact your IT department for help.</span></span> <span data-ttu-id="344b4-145">사용자 설정을 삭제하도록 하면 다음 번에 로그인할 때 [2단계 인증 등록](multi-factor-authentication-end-user-first-time.md) 메시지가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-145">Have them clear your settings so the next time you sign in, you will be prompted to [register for two-step verification](multi-factor-authentication-end-user-first-time.md) again.</span></span>

## <a name="i-am-not-receiving-a-text-or-call-on-my-phone"></a><span data-ttu-id="344b4-146">휴대폰에서 텍스트 메시지를 받지 못하는 경우</span><span class="sxs-lookup"><span data-stu-id="344b4-146">I am not receiving a text or call on my phone</span></span>
<span data-ttu-id="344b4-147">로그인하지만 텍스트 또는 전화 통화를 수신하지는 않으려는 여러 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-147">There are several reasons why you may try to sign in, but not receive the text or phone call.</span></span> <span data-ttu-id="344b4-148">이전에 전화에 텍스트 또는 전화 통화를 성공적으로 수신한 경우에는 사용자 계정이 아니라 전화 공급자와 관련된 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-148">If you've successfully received texts or phone calls to your phone in the past, then this is probably an issue with the phone provider, not your account.</span></span> <span data-ttu-id="344b4-149">휴대 전화 신호가 양호한지 확인하고 텍스트 메시지를 수신하려는 경우 텍스트 메시지를 수신할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-149">Make sure that you have good cell signal, and if you are trying to receive a text message make sure that you are able to recieve text messages.</span></span> <span data-ttu-id="344b4-150">테스트 삼아 친구에게 통화 또는 문자를 보내달라고 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-150">Ask a friend to call you or text you as a test.</span></span> 

<span data-ttu-id="344b4-151">텍스트 또는 전화를 몇 분 정도 기다린 경우 빠르게 계정에 액세스하는 방법은 다른 옵션을 시도하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-151">If you've waited several minutes for a text or call, the fastest way to get into your account is to try a different option.</span></span>

1. <span data-ttu-id="344b4-152">페이지에서 **다른 인증 옵션 사용**을 선택하고 인증을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-152">Select **Use a different verification option** on the page that's waiting for your verification.</span></span>
   
    ![다양한 확인](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)
2. <span data-ttu-id="344b4-154">사용하려는 전화 번호 또는 배달 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-154">Select the phone number or delivery method you want to use.</span></span>
   
    <span data-ttu-id="344b4-155">여러 인증 코드를 받은 경우 최신 코드만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-155">If you received multiple verification codes, use the newest one.</span></span>

<span data-ttu-id="344b4-156">다른 방법을 구성하지 않은 경우 IT 부서에게 문의하고 설정을 지우도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-156">If you don’t have another method configured, contact your IT department and ask them to clear your settings.</span></span> <span data-ttu-id="344b4-157">다음 번 로그인할 때 다시 [Multi-Factor Authentication 설정](multi-factor-authentication-end-user-first-time.md)하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-157">The next time you sign in, you will be prompted to [set up multi-factor authentication](multi-factor-authentication-end-user-first-time.md) again.</span></span>

<span data-ttu-id="344b4-158">종종 잘못된 셀 신호로 인해 지연된 경우 스마트폰에서 [Microsoft Authenticator 앱](microsoft-authenticator-app-how-to.md)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-158">If you often have delays due to bad cell signal, we recommend you use the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) on your smartphone.</span></span> <span data-ttu-id="344b4-159">앱은 로그인하는 데 사용할 수 있는 임의의 보안 코드를 생성할 수 있고 이러한 코드는 셀 신호 또는 인터넷 연결이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-159">The app can generate random security codes that you use to sign in, and these codes don't require any cell signal or internet connection.</span></span>

## <a name="app-passwords-are-not-working"></a><span data-ttu-id="344b4-160">앱 암호가 작동하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="344b4-160">App passwords are not working</span></span>
<span data-ttu-id="344b4-161">먼저 앱 암호를 올바르게 입력했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-161">First, make sure that you have entered the app password correctly.</span></span> <span data-ttu-id="344b4-162">2단계 인증을 지원하지 않는 이전 데스크톱 응용 프로그램의 경우에만 생성된 앱 암호가 사용자의 일반 암호를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-162">The generated app password replaces your normal password, but only for older desktop applications that don't support two-step verification.</span></span> <span data-ttu-id="344b4-163">계속 작동하지 않으면 로그인을 시도하고 [새 앱 암호를 생성](multi-factor-authentication-end-user-app-passwords.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-163">If it still isn't working, try signing-in and [create a new app password](multi-factor-authentication-end-user-app-passwords.md).</span></span>  <span data-ttu-id="344b4-164">계속 작동하지 않으면 IT 부서에 문의하여 [사용자의 기존 앱 암호를 삭제](../multi-factor-authentication-manage-users-and-devices.md)하도록 요청하면 새 암호를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-164">If it still doesn't work, contact your IT department and have them [delete your existing app passwords](../multi-factor-authentication-manage-users-and-devices.md) and then you can create a new one.</span></span>

## <a name="i-didnt-find-an-answer-to-my-problem"></a><span data-ttu-id="344b4-165">문제에 대한 답변을 찾을 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="344b4-165">I didn't find an answer to my problem.</span></span>
<span data-ttu-id="344b4-166">이러한 문제 해결 단계를 시도했는데도 문제가 계속되는 경우 IT 부서에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="344b4-166">If you've tried these troubleshooting steps but are still running into problems, contact your IT department.</span></span> <span data-ttu-id="344b4-167">그러면 도움을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="344b4-167">They should be able to assist you.</span></span>

## <a name="related-topics"></a><span data-ttu-id="344b4-168">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="344b4-168">Related topics</span></span>
* [<span data-ttu-id="344b4-169">2단계 인증을 위한 설정 관리</span><span class="sxs-lookup"><span data-stu-id="344b4-169">Manage your settings for two-step verification</span></span>](multi-factor-authentication-end-user-manage-settings.md)  
* [<span data-ttu-id="344b4-170">Microsoft Authenticator 응용 프로그램 FAQ</span><span class="sxs-lookup"><span data-stu-id="344b4-170">Microsoft Authenticator application FAQ</span></span>](microsoft-authenticator-app-faq.md)


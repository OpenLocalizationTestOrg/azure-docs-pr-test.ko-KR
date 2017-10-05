---
title: "2단계 인증을 통한 Azure MFA 로그인 | Microsoft Docs"
description: "이 페이지에서는 Azure MFA에서 사용할 수 있는 다양한 로그인 방법을 확인할 수 있는 위치에 대한 지침을 제공합니다."
keywords: "사용자 인증, 로그인 환경, 휴대폰으로 로그인, 사무실 전화로 로그인"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: d12115be61ca00dfb86dd822ccae9f9096fa796a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="the-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="7382d-104">Azure Multi-Factor Authentication의 로그인 환경</span><span class="sxs-lookup"><span data-stu-id="7382d-104">The sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="7382d-105">이 문서의 목적은 일반적인 로그인 환경을 연습해보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-105">The purpose of this article is to walk through a typical sign-in experience.</span></span> <span data-ttu-id="7382d-106">로그인 관련 지원을 얻거나 문제를 해결하려면 [Azure Multi-Factor Authentication에 문제가 있는 경우](multi-factor-authentication-end-user-troubleshoot.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7382d-106">For help with signing in, or to troubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="7382d-107">어떤 로그인 환경이 제공되나요?</span><span class="sxs-lookup"><span data-stu-id="7382d-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="7382d-108">두 번째 단계로 사용하도록 선택하는 항목(예: 전화 통화, 인증 앱 또는 문자)에 따라 로그인 환경이 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-108">Your sign-in experience differs depending on what you choose to use as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="7382d-109">수행하는 작업을 가장 잘 설명하는 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-109">Choose the option that best describes what you are doing:</span></span>

| <span data-ttu-id="7382d-110">로그인하는 방법</span><span class="sxs-lookup"><span data-stu-id="7382d-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="7382d-111">내 휴대폰 또는 사무실 전화로 통화</span><span class="sxs-lookup"><span data-stu-id="7382d-111">With a phone call to my mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="7382d-112">내 휴대폰으로 문자 발송</span><span class="sxs-lookup"><span data-stu-id="7382d-112">With a text to my mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="7382d-113"> 앱의 알림 사용</span><span class="sxs-lookup"><span data-stu-id="7382d-113">With notifications from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="7382d-114">Microsoft Authenticator 앱의 확인 코드 사용</span><span class="sxs-lookup"><span data-stu-id="7382d-114">With verification codes from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="7382d-115">원하는 방법이 없으므로 다른 방법 사용</span><span class="sxs-lookup"><span data-stu-id="7382d-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="7382d-116">전화 통화를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="7382d-116">Signing in with a phone call</span></span>
<span data-ttu-id="7382d-117">다음 정보에서는 휴대폰 또는 사무실 전화 통화를 사용한 2단계 확인 환경에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-117">The following information describes the two-step verification experience with a call to your mobile or office phone.</span></span>

1. <span data-ttu-id="7382d-118">사용자 이름 및 암호를 사용하여 Office 365와 같은 응용 프로그램 또는 서비스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-118">Sign in to an application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="7382d-119">Microsoft에서 전화를 합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="7382d-120">전화를 받고 # 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-120">Answer the phone and hit the # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="7382d-121">문자 메시지를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="7382d-121">Signing in with a text message</span></span>
<span data-ttu-id="7382d-122">다음 정보에서는 휴대폰으로 문자 메시지를 발송하는 2단계 확인 환경에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-122">The following information describes the two-step verification experience with a text message to your mobile phone:</span></span>

1. <span data-ttu-id="7382d-123">사용자 이름 및 암호를 사용하여 Office 365와 같은 응용 프로그램 또는 서비스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-123">Sign in to an application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="7382d-124">Microsoft에서 숫자 코드를 포함하는 문자 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="7382d-125">로그인 페이지에 제공된 상자에 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-125">Enter the code in the box provided on the sign-in page.</span></span> 

## <a name="signing-in-with-the-microsoft-authenticator-app"></a><span data-ttu-id="7382d-126">Microsoft Authenticator 앱에 로그인</span><span class="sxs-lookup"><span data-stu-id="7382d-126">Signing in with the Microsoft Authenticator app</span></span> 
<span data-ttu-id="7382d-127">다음 정보는 2단계 확인을 위해 Microsoft Authenticator 앱을 사용하는 환경을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-127">The following information describes the experience of using the Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="7382d-128">앱을 사용하는 두 가지 다른 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-128">There are two different ways to use the app.</span></span> <span data-ttu-id="7382d-129">장치에서 푸시 알림을 받거나 앱을 열어 확인 코드를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-129">You can receive push notifications on your device, or you can open the app to get a verification code.</span></span>

### <a name="to-sign-in-with-a-notification-from-the-microsoft-authenticator-app"></a><span data-ttu-id="7382d-130">Microsoft Authenticator 앱의 인증으로 로그인하려면</span><span class="sxs-lookup"><span data-stu-id="7382d-130">To sign in with a notification from the Microsoft Authenticator app</span></span>
1. <span data-ttu-id="7382d-131">사용자 이름 및 암호를 사용하여 Office 365와 같은 응용 프로그램 또는 서비스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-131">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="7382d-132">Microsoft는 사용자 장치의 Microsoft Authenticator 앱에 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-132">Microsoft sends a notification to the Microsoft Authenticator app on your device.</span></span>

  ![Microsoft가 알림을 보냄](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="7382d-134">휴대폰에서 알림을 열고 **확인** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-134">Open the notification on your phone and select the **Verify** key.</span></span> <span data-ttu-id="7382d-135">회사에서 PIN을 요구하는 경우 여기에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="7382d-136">사용자가 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-136">You should now be signed in.</span></span>

### <a name="to-sign-in-using-a-verification-code-with-the-microsoft-authenticator-app"></a><span data-ttu-id="7382d-137">확인 코드를 사용하여 Microsoft Authenticator 앱에 로그인하려면</span><span class="sxs-lookup"><span data-stu-id="7382d-137">To sign in using a verification code with the Microsoft Authenticator app</span></span>

<span data-ttu-id="7382d-138">Microsoft Authenticator 앱을 사용하여 확인 코드를 가져오는 경우 앱을 열 때 계정 이름 아래에 숫자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-138">If you use the Microsoft Authenticator app to get verification codes, then when you open the app you see a number under your account name.</span></span> <span data-ttu-id="7382d-139">이 숫자는 같은 숫자를 두 번 사용하는 일이 없도록 30초마다 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-139">This number changes every 30 seconds so that you don't use the same number twice.</span></span> <span data-ttu-id="7382d-140">확인 코드를 묻는 메시지가 표시되면 앱을 열고 현재 표시되는 숫자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-140">When you're asked for a verification code, open the app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="7382d-141">사용자 이름 및 암호를 사용하여 Office 365와 같은 응용 프로그램 또는 서비스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-141">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="7382d-142">Microsoft가 확인 코드를 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-142">Microsoft prompts you for a verification code.</span></span>

  ![확인 코드 입력](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="7382d-144">휴대폰에서 Microsoft Authenticator 앱을 열고 로그인 위치에 제공되는 상자에 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-144">Open the Microsoft Authenticator app on your phone and enter the code in the box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="7382d-145">다른 방법을 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="7382d-145">Signing in with an alternate method</span></span>
<span data-ttu-id="7382d-146">경우에 따라 기본 확인 방법으로 설정한 휴대폰이나 장치가 없는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-146">Sometimes you don't have the phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="7382d-147">계정에 대해 백업 방법을 설정하도록 권장하는 것도 이 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="7382d-148">다음 섹션에서는 기본 방법을 사용할 수 없을 때 대체 방법을 사용하여 로그인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-148">The following section shows you how to sign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="7382d-149">사용자 이름 및 암호를 사용하여 Office 365와 같은 응용 프로그램 또는 서비스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-149">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="7382d-150">**다른 확인 옵션 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="7382d-151">설정한 수에 따라 다른 확인 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="7382d-152">대체 방법을 선택하고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7382d-152">Choose an alternate method and sign in.</span></span>

  ![대체 방법 사용](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="7382d-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7382d-154">Next steps</span></span>

<span data-ttu-id="7382d-155">2단계 확인을 사용하여 로그인하는 동안 문제가 발생하면 [Azure Multi-Factor Authentication에 문제가 있는 경우](multi-factor-authentication-end-user-troubleshoot.md)에서 자세한 정보를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7382d-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="7382d-156">[2단계 확인 설정 관리](multi-factor-authentication-end-user-manage-settings.md) 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="7382d-156">Learn how to [Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="7382d-157">문자 메시지 및 전화 대신 알림을 사용하여 로그인할 수 있도록 [Microsoft Authenticator 앱 시작](microsoft-authenticator-app-how-to.md) 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7382d-157">Find out how to [Get started with the Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications to sign in, instead of texts and phone calls.</span></span> 
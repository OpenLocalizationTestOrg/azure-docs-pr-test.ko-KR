---
title: "MFA aaaAzure 로그인 2 단계 확인 | Microsoft Docs"
description: "이 페이지 있습니다 지침을 제공 합니다 여기서 toogo toosee hello 다양 한 로그인 방법이 Azure MFA를 사용할 수 있습니다."
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
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="42f1d-104">Azure Multi-factor authentication hello 로그인 환경</span><span class="sxs-lookup"><span data-stu-id="42f1d-104">hello sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="42f1d-105">hello이 문서의 목적은 일반적인 로그인 환경을 통해 toowalk입니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-105">hello purpose of this article is toowalk through a typical sign-in experience.</span></span> <span data-ttu-id="42f1d-106">로그인 또는 tootroubleshoot 문제 관련 도움말을 참조 [Azure Multi-factor Authentication에 문제가](multi-factor-authentication-end-user-troubleshoot.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-106">For help with signing in, or tootroubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="42f1d-107">어떤 로그인 환경이 제공되나요?</span><span class="sxs-lookup"><span data-stu-id="42f1d-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="42f1d-108">사용자 로그인 환경에 선택한 항목 toouse에 두 번째 요소로 따라 달라 집니다: 전화 통화, 인증 앱을 사용할지 아니면 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-108">Your sign-in experience differs depending on what you choose toouse as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="42f1d-109">가장 잘 진행 중에 작업을 설명 하는 hello 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-109">Choose hello option that best describes what you are doing:</span></span>

| <span data-ttu-id="42f1d-110">로그인하는 방법</span><span class="sxs-lookup"><span data-stu-id="42f1d-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="42f1d-111">전화 통화 toomy 휴대폰 / 사무실 전화</span><span class="sxs-lookup"><span data-stu-id="42f1d-111">With a phone call toomy mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="42f1d-112">Toomy 휴대폰 문자 사용</span><span class="sxs-lookup"><span data-stu-id="42f1d-112">With a text toomy mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="42f1d-113">Hello Microsoft 인증자 앱에서 알림</span><span class="sxs-lookup"><span data-stu-id="42f1d-113">With notifications from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="42f1d-114">Hello Microsoft 인증자 앱에서 확인 코드 사용</span><span class="sxs-lookup"><span data-stu-id="42f1d-114">With verification codes from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="42f1d-115">원하는 방법이 없으므로 다른 방법 사용</span><span class="sxs-lookup"><span data-stu-id="42f1d-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="42f1d-116">전화 통화를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="42f1d-116">Signing in with a phone call</span></span>
<span data-ttu-id="42f1d-117">다음 정보는 hello 호출 tooyour 모바일 경험이 2 단계 확인 hello 또는 사무실 전화를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-117">hello following information describes hello two-step verification experience with a call tooyour mobile or office phone.</span></span>

1. <span data-ttu-id="42f1d-118">Tooan 응용 프로그램 또는 사용자 이름 및 암호를 사용 하 여 Office 365와 같은 서비스에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-118">Sign in tooan application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="42f1d-119">Microsoft에서 전화를 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="42f1d-120">Hello 전화에 답변 하 고 hello # 키를 누르십시오.</span><span class="sxs-lookup"><span data-stu-id="42f1d-120">Answer hello phone and hit hello # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="42f1d-121">문자 메시지를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="42f1d-121">Signing in with a text message</span></span>
<span data-ttu-id="42f1d-122">다음 정보는 hello 메시지 tooyour 텍스트 휴대폰 경험이 2 단계 확인 hello를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-122">hello following information describes hello two-step verification experience with a text message tooyour mobile phone:</span></span>

1. <span data-ttu-id="42f1d-123">Tooan 응용 프로그램 또는 사용자 이름 및 암호를 사용 하 여 Office 365와 같은 서비스에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-123">Sign in tooan application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="42f1d-124">Microsoft에서 숫자 코드를 포함하는 문자 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="42f1d-125">Hello 로그인 페이지에 제공 된 hello 상자에 hello 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-125">Enter hello code in hello box provided on hello sign-in page.</span></span> 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="42f1d-126">Hello Microsoft Authenticator 앱을 사용 하 여 로그인</span><span class="sxs-lookup"><span data-stu-id="42f1d-126">Signing in with hello Microsoft Authenticator app</span></span> 
<span data-ttu-id="42f1d-127">hello 다음 설명 hello Microsoft Authenticator 앱을 사용 하 여 2 단계 확인 작업에 대 한 hello 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-127">hello following information describes hello experience of using hello Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="42f1d-128">두 가지 방법으로 toouse hello 앱 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-128">There are two different ways toouse hello app.</span></span> <span data-ttu-id="42f1d-129">사용자의 장치에 푸시 알림을 받을 수 있습니다 또는 hello 앱 tooget 확인 코드를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-129">You can receive push notifications on your device, or you can open hello app tooget a verification code.</span></span>

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a><span data-ttu-id="42f1d-130">hello Microsoft 인증자 앱에서 알림 사용 하 여 toosign</span><span class="sxs-lookup"><span data-stu-id="42f1d-130">toosign in with a notification from hello Microsoft Authenticator app</span></span>
1. <span data-ttu-id="42f1d-131">Tooan 응용 프로그램 또는 사용자 이름 및 암호를 사용 하 여 Office 365와 같은 서비스에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-131">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="42f1d-132">Microsoft는 장치에서 알림 toohello Microsoft Authenticator 앱을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-132">Microsoft sends a notification toohello Microsoft Authenticator app on your device.</span></span>

  ![Microsoft가 알림을 보냄](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="42f1d-134">전화 및 선택 hello에 대 한 열기 hello 알림 **확인** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-134">Open hello notification on your phone and select hello **Verify** key.</span></span> <span data-ttu-id="42f1d-135">회사에서 PIN을 요구하는 경우 여기에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="42f1d-136">사용자가 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-136">You should now be signed in.</span></span>

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="42f1d-137">확인 코드를 사용 하 여 hello Microsoft Authenticator 앱과 toosign</span><span class="sxs-lookup"><span data-stu-id="42f1d-137">toosign in using a verification code with hello Microsoft Authenticator app</span></span>

<span data-ttu-id="42f1d-138">Hello Microsoft Authenticator 앱 tooget 확인 코드를 사용 하는 경우 다음 hello 앱을 열 때 표시 숫자 계정 이름.</span><span class="sxs-lookup"><span data-stu-id="42f1d-138">If you use hello Microsoft Authenticator app tooget verification codes, then when you open hello app you see a number under your account name.</span></span> <span data-ttu-id="42f1d-139">이 수 동일 수를 두 번 hello를 사용 하지 않는 하도록 30 초 마다 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-139">This number changes every 30 seconds so that you don't use hello same number twice.</span></span> <span data-ttu-id="42f1d-140">확인 코드를 묻는 경우 hello 앱 열고 수에 관계 없이 현재 표시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-140">When you're asked for a verification code, open hello app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="42f1d-141">Tooan 응용 프로그램 또는 사용자 이름 및 암호를 사용 하 여 Office 365와 같은 서비스에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-141">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="42f1d-142">Microsoft가 확인 코드를 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-142">Microsoft prompts you for a verification code.</span></span>

  ![확인 코드 입력](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="42f1d-144">휴대폰에서 hello Microsoft Authenticator 앱을 열고 hello 상자에 로그인 하는 위치에 hello 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-144">Open hello Microsoft Authenticator app on your phone and enter hello code in hello box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="42f1d-145">다른 방법을 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="42f1d-145">Signing in with an alternate method</span></span>
<span data-ttu-id="42f1d-146">경우에 따라 hello 전화 번호 또는 기본 설정된 확인 방법으로 설정 하는 장치 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-146">Sometimes you don't have hello phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="42f1d-147">계정에 대해 백업 방법을 설정하도록 권장하는 것도 이 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="42f1d-148">hello 다음 섹션에서는 기본 방법을 사용 하지 못할 경우 다른 방법 사용 하 여 toosign 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-148">hello following section shows you how toosign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="42f1d-149">Tooan 응용 프로그램 또는 사용자 이름 및 암호를 사용 하 여 Office 365와 같은 서비스에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-149">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="42f1d-150">**다른 확인 옵션 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="42f1d-151">설정한 수에 따라 다른 확인 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="42f1d-152">대체 방법을 선택하고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-152">Choose an alternate method and sign in.</span></span>

  ![대체 방법 사용](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="42f1d-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42f1d-154">Next steps</span></span>

<span data-ttu-id="42f1d-155">2단계 확인을 사용하여 로그인하는 동안 문제가 발생하면 [Azure Multi-Factor Authentication에 문제가 있는 경우](multi-factor-authentication-end-user-troubleshoot.md)에서 자세한 정보를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="42f1d-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="42f1d-156">너무 방법에 대해 알아봅니다[2 단계 확인 설정 관리](multi-factor-authentication-end-user-manage-settings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-156">Learn how too[Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="42f1d-157">너무 방법을 보려면[hello Microsoft Authenticator 앱 시작](microsoft-authenticator-app-how-to.md) 알림 toosign, 텍스트 및 전화 통화가 대신 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="42f1d-157">Find out how too[Get started with hello Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications toosign in, instead of texts and phone calls.</span></span> 

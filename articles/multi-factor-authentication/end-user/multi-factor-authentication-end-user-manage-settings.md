---
title: "2단계 인증 설정 관리 | Microsoft Docs"
description: "연락처 정보를 변경하거나 장치를 구성하는 등 Azure Multi-Factor Authentication을 사용하는 방법을 관리합니다."
services: multi-factor-authentication
keywords: "다단계 인증 클라이언트, 인증 문제, 상관관계 ID"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: f752fb19e4ff2f831d50104e9c7d5f42cc3486d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a><span data-ttu-id="4c1eb-104">2단계 인증을 위한 설정 관리</span><span class="sxs-lookup"><span data-stu-id="4c1eb-104">Manage your settings for two-step verification</span></span>
<span data-ttu-id="4c1eb-105">이 문서에서는 2단계 인증 또는 다단계 인증에 대한 설정을 업데이트하는 방법에 대한 질문에 대답합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-105">This article answers questions about how to update settings for two-step verification or multi-factor authentication.</span></span> <span data-ttu-id="4c1eb-106">계정에 로그인하는 데 문제가 있는 경우 문제 해결 도움말을 보려면 [2단계 인증에 문제 발생](multi-factor-authentication-end-user-troubleshoot.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-106">If you are having issues signing in to your account, refer to [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md) for troubleshooting help.</span></span>

## <a name="where-to-find-the-settings-page"></a><span data-ttu-id="4c1eb-107">설정 페이지 위치</span><span class="sxs-lookup"><span data-stu-id="4c1eb-107">Where to find the settings page</span></span>
<span data-ttu-id="4c1eb-108">회사에서 Azure Multi-Factor Authentication을 설정하는 방법에 따라 전화 번호와 같은 설정을 변경할 수 있는 몇 가지 위치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-108">Depending on how your company set up Azure Multi-Factor Authentication, there are a few places where you can change your settings like your phone number.</span></span>

<span data-ttu-id="4c1eb-109">IT 관리자가 2단계 인증을 관리하기 위한 특정 URL 또는 단계를 전송한 경우 해당 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-109">If your IT admin sent out a specific URL or steps to manage two-step verification, follow those instructions.</span></span> <span data-ttu-id="4c1eb-110">그렇지 않으면 다른 모든 사용자는 다음 지침을 따르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-110">Otherwise, the following instructions should work for everybody else.</span></span> <span data-ttu-id="4c1eb-111">이러한 지침을 따랐지만 동일한 옵션이 표시되지 않는다면 회사 또는 학교에서 고유한 포털을 사용자 지정했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-111">If you follow these steps but don't see the same options, that means that your work or school customized their own portal.</span></span> <span data-ttu-id="4c1eb-112">관리자에게 Azure Multi-Factor Authentication 포털에 대한 링크 요청</span><span class="sxs-lookup"><span data-stu-id="4c1eb-112">Ask your admin for the link to your Azure Multi-Factor Authentication portal.</span></span>

1. <span data-ttu-id="4c1eb-113">[https://myapps.microsoft.com](https://myapps.microsoft.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-113">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>  
2. <span data-ttu-id="4c1eb-114">오른쪽 맨 위에서 계정 이름을 선택한 후 **프로필**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-114">Select your account name in the top right, then select **profile**.</span></span>  
3. <span data-ttu-id="4c1eb-115">**추가 보안 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-115">Select **Additional security verification**.</span></span>  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. <span data-ttu-id="4c1eb-117">추가 보안 인증 페이지에 설정이 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-117">The Additional security verification page loads with your settings.</span></span>

    ![검사](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-to-change-my-phone-number-or-add-a-secondary-number"></a><span data-ttu-id="4c1eb-119">휴대폰 번호를 변경하거나 보조 번호를 추가하려는 경우</span><span class="sxs-lookup"><span data-stu-id="4c1eb-119">I want to change my phone number, or add a secondary number</span></span>
<span data-ttu-id="4c1eb-120">보조 인증 전화 번호를 구성하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-120">It is important to configure a secondary authentication phone number.</span></span>  <span data-ttu-id="4c1eb-121">기본 전화 번호 및 모바일 앱은 아마도 동일한 전화상에 있으므로 보조 전화 번호는 전화를 분실하거나 도난당한 경우 사용자 계정으로 돌아갈 수 있는 유일한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-121">Because your primary phone number and your mobile app are probably on the same phone, the secondary phone number is the only way you will be able to get back into your account if your phone is lost or stolen.</span></span>

> [!NOTE]
> <span data-ttu-id="4c1eb-122">기본 전화 번호에 대한 액세스 권한이 없고 계정에 대한 도움이 필요한 경우 [2단계 인증에 문제 발생](multi-factor-authentication-end-user-troubleshoot.md)에서 도움말 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-122">If you don't have access to your primary phone number, and need help getting in to your account, see our help topics in [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md).</span></span>  

<span data-ttu-id="4c1eb-123">**기본 전화 번호를 변경하려면:**</span><span class="sxs-lookup"><span data-stu-id="4c1eb-123">**To change your primary phone number:**</span></span>  

1. <span data-ttu-id="4c1eb-124">추가 보안 인증 페이지에서 현재 전화 번호가 있는 텍스트 상자를 선택하고 새 전화 번호로 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-124">On the Additional security verification page, select the text box with your current phone number and edit it with your new phone number.</span></span>  
2. <span data-ttu-id="4c1eb-125">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-125">Select **Save**.</span></span>  
3. <span data-ttu-id="4c1eb-126">기본 설정된 인증 옵션에 사용할 번호인 경우 저장하기 전에 새 번호를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-126">If this is the number that you use for your preferred verification option, you have to verify the new number before you can save it.</span></span>  

<span data-ttu-id="4c1eb-127">**보조 번호를 추가하려면:**</span><span class="sxs-lookup"><span data-stu-id="4c1eb-127">**To add a secondary phone number:**</span></span>  

1. <span data-ttu-id="4c1eb-128">추가 보안 인증 페이지에서 **대체 인증 전화** 옆의 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-128">On the Additional security verification page, check the box next to **Alternate authentication phone.**</span></span>  
2. <span data-ttu-id="4c1eb-129">텍스트 상자에 보조 전화 번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-129">Enter your secondary phone number in the text box.</span></span>  
3. <span data-ttu-id="4c1eb-130">**저장**을 선택하면 변경 내용이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-130">Select **Save** and your changes are finished.</span></span>  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a><span data-ttu-id="4c1eb-131">신뢰할 수 있는 것으로 표시된 장치에서 2단계 인증이 다시 필요</span><span class="sxs-lookup"><span data-stu-id="4c1eb-131">Require two-step verification again on a device you've marked as trusted</span></span>

<span data-ttu-id="4c1eb-132">조직 설정에 따라 브라우저에서 2단계 인증을 수행할 때 "**X**일 동안 다시 묻지 않음"이라는 확인란이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-132">Depending on your organization settings, you may have a checkbox that says "Don't ask again for **X** days" when you perform two-step verification on your browser.</span></span> <span data-ttu-id="4c1eb-133">이 확인란을 선택한 후 장치를 분실하거나 계정이 손상된 것으로 생각되는 경우 2단계 인증을 모든 장치로 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-133">If you check this box and then lose your device or think that your account is compromised, you should restore two-step verification to all your devices.</span></span> 

1. <span data-ttu-id="4c1eb-134">추가 보안 확인 페이지에서 **이전에 신뢰할 수 있는 장치에서 Multi-Factor Authentication 복원**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-134">On the Additional security verification page, select **Restore multi-factor authentication on previously trusted devices**.</span></span>
2. <span data-ttu-id="4c1eb-135">장치에 다음에 로그인하면 2단계 인증을 수행하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-135">The next time you sign in on any device, you'll be prompted to perform two-step verification.</span></span> 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-to-a-new-one"></a><span data-ttu-id="4c1eb-136">이전 장치에서 Microsoft Authenticator를 제거하고 새 장치로 이동하려는 경우</span><span class="sxs-lookup"><span data-stu-id="4c1eb-136">How do I clean up Microsoft Authenticator from my old device and move to a new one?</span></span>
<span data-ttu-id="4c1eb-137">장치에서 앱을 제거하거나 장치를 재설정하는 경우 백 엔드에서 정품 인증을 제거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-137">When you uninstall the app from your device or reset the device, it does not remove the activation on the back end.</span></span> <span data-ttu-id="4c1eb-138">자세한 내용은 [Microsoft Authenticator](microsoft-authenticator-app-how-to.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-138">For more information, see [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c1eb-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c1eb-139">Next steps</span></span>
* <span data-ttu-id="4c1eb-140">[2단계 인증에 문제 발생](multi-factor-authentication-end-user-troubleshoot.md)에 대한 문제 해결 팁 및 도움말 얻기</span><span class="sxs-lookup"><span data-stu-id="4c1eb-140">Get troubleshooting tips and help on [Having trouble with two-step verification](multi-factor-authentication-end-user-troubleshoot.md)</span></span>
* <span data-ttu-id="4c1eb-141">2단계 인증을 지원하지 않는 앱에 대해 [앱 암호](multi-factor-authentication-end-user-app-passwords.md) 설정.</span><span class="sxs-lookup"><span data-stu-id="4c1eb-141">Set up [app passwords](multi-factor-authentication-end-user-app-passwords.md) for any apps that don't support two-step verification.</span></span>

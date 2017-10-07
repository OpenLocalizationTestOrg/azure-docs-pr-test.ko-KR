---
title: "빠른 시작: Azure AD SSPR | Microsoft Docs"
description: "신속하게 Azure AD 셀프 서비스 암호 재설정 배포"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a><span data-ttu-id="1bec9-103">빠른 시작: Azure AD 셀프 서비스 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="1bec9-103">Quickstart: Azure AD self-service password reset</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1bec9-104">**로그인하는 데 문제가 있나요?**</span><span class="sxs-lookup"><span data-stu-id="1bec9-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="1bec9-105">그렇다면 [암호를 변경하고 재설정하는 방법은 다음과 같습니다](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="1bec9-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md).</span></span>

## <a name="rapidly-deploy-self-service-password-reset"></a><span data-ttu-id="1bec9-106">신속하게 셀프 서비스 암호 재설정 배포</span><span class="sxs-lookup"><span data-stu-id="1bec9-106">Rapidly deploy self-service password reset</span></span>

<span data-ttu-id="1bec9-107">셀프 서비스 암호 재설정 (SSPR)는 단순 일정 또는 IT 관리자가 tooempower 사용자 tooreset에 대 한 의미의 암호나 계정을 잠금 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-107">Self-service password reset (SSPR) offers a simple means for IT administrators tooempower users tooreset or unlock their passwords or accounts.</span></span> <span data-ttu-id="1bec9-108">hello 시스템에 자세한 보고 tootrack 사용자가 알림 tooalert 함께 hello 시스템을 사용 하면 toomisuse 또는 사용상 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-108">hello system includes detailed reporting tootrack when users use hello system along with notifications tooalert you toomisuse or abuse.</span></span>

<span data-ttu-id="1bec9-109">이 가이드에서는 이미 여러분이 작업 평가판 또는 사용이 허가된 Azure AD 테넌트를 갖고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-109">This guide assumes you already have a working trial or licensed Azure AD tenant.</span></span> <span data-ttu-id="1bec9-110">Azure AD 설정 시 도움이 필요한 경우 hello 문서 참조 [Azure AD 시작](https://azure.microsoft.com/trial/get-started-active-directory/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-110">If you need help setting up Azure AD, see hello article [Getting Started with Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/).</span></span>

1. <span data-ttu-id="1bec9-111">기존 Azure AD 테넌트에서 **"암호 재설정"**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-111">From your existing Azure AD tenant, select **"Password reset"**</span></span>

2. <span data-ttu-id="1bec9-112">Hello에서 **"속성"** hello 다음 중 하나를 선택 "셀프 서비스 암호 재설정 사용" hello 옵션 아래에서 화면</span><span class="sxs-lookup"><span data-stu-id="1bec9-112">From hello **"Properties"** screen, under hello option "Self Service Password Reset Enabled" choose one of hello following</span></span>
    * <span data-ttu-id="1bec9-113">아무도-아무도 수 toouse SSPR 기능</span><span class="sxs-lookup"><span data-stu-id="1bec9-113">Nobody - No one is able toouse SSPR functionality</span></span>
    * <span data-ttu-id="1bec9-114">그룹-만 특정 Azure AD의 그룹 구성원 선택 하는 수 toouse SSPR 기능</span><span class="sxs-lookup"><span data-stu-id="1bec9-114">A group - Only members of a specific Azure AD group that you choose are able toouse SSPR functionality</span></span>
    * <span data-ttu-id="1bec9-115">모든 사용자에 게-Azure AD 테 넌 트에 계정이 있는 모든 사용자는 수 toouse SSPR 기능</span><span class="sxs-lookup"><span data-stu-id="1bec9-115">Everybody - All users with accounts in your Azure AD tenant are able toouse SSPR functionality</span></span>

3. <span data-ttu-id="1bec9-116">Hello에서 **"인증 방법"** 선택 화면</span><span class="sxs-lookup"><span data-stu-id="1bec9-116">From hello **"Authentication methods"** screen choose</span></span>
    * <span data-ttu-id="1bec9-117">다양 한 방법 필수 tooreset-적어도 하나 또는 두 개의 최대 지원</span><span class="sxs-lookup"><span data-stu-id="1bec9-117">Number of methods required tooreset - We support a minimum of one or a maximum of two</span></span>
    * <span data-ttu-id="1bec9-118">메서드 사용 가능한 toousers-하나 이상의 하지만 알아보는 것이 toohave 사용할 수 있는 추가 선택</span><span class="sxs-lookup"><span data-stu-id="1bec9-118">Methods available toousers - We need at least one but it never hurts toohave an extra choice available</span></span>
        * <span data-ttu-id="1bec9-119">**전자 메일** 코드 toohello 사용자와 전자 메일의 인증 전자 메일 주소를 구성 하는 전송</span><span class="sxs-lookup"><span data-stu-id="1bec9-119">**Email** sends an email with a code toohello user's configured authentication email address</span></span>
        * <span data-ttu-id="1bec9-120">**휴대폰** 제공 hello 사용자 hello 선택 tooreceive 호출 또는 텍스트를 코드 tootheir 모바일 전화 번호 구성</span><span class="sxs-lookup"><span data-stu-id="1bec9-120">**Mobile Phone** gives hello user hello choice tooreceive a call or text with a code tootheir configured mobile phone number</span></span>
        * <span data-ttu-id="1bec9-121">**사무실 전화** 코드 tootheir 있는 호출 hello 사용자 구성 사무실 전화 번호</span><span class="sxs-lookup"><span data-stu-id="1bec9-121">**Office Phone** calls hello user with a code tootheir configured office phone number</span></span>
        * <span data-ttu-id="1bec9-122">**보안 질문** toochoose 해야</span><span class="sxs-lookup"><span data-stu-id="1bec9-122">**Security Questions** requires you toochoose</span></span>
            * <span data-ttu-id="1bec9-123">Tooregister는 데 필요한 질문 수-의미 사용자 등록을 성공적으로 대 한 hello 최소 tooanswer의 풀에서 toopull 질문 자세한 toocreate 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-123">Number of questions required tooregister - hello minimum for successful registration, meaning a user can choose tooanswer more toocreate a pool of questions toopull from.</span></span> <span data-ttu-id="1bec9-124">이 옵션 3-5에서 설정할 수 있습니다 및 보다 클 수 하거나 질문 필요한 tooreset toohello 수가 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-124">This option can be set from 3-5 and must be greater than or equal toohello number of questions required tooreset.</span></span>
                * <span data-ttu-id="1bec9-125">보안 질문을 선택 하는 경우에 hello "Custom" 단추를 클릭 하 여 사용자 지정 질문을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-125">Custom questions can be added by clicking hello "Custom" button when selecting security questions</span></span>
            * <span data-ttu-id="1bec9-126">필요한 질문 수 tooreset-3-5 질문 toobe 사용자 암호 toobe 다시 설정 하거나 잠금 해제를 허용 하기 전에 올바르게 대답에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-126">Number of questions required tooreset - Can be set from 3-5 questions toobe answered correctly before allowing a users password toobe reset or unlocked.</span></span>

4. <span data-ttu-id="1bec9-127">권장: **"사용자 지정"** 있습니다 toochange hello "관리자에 게 문의" 링크 toopoint tooa 페이지 또는 전자 메일 주소 정의</span><span class="sxs-lookup"><span data-stu-id="1bec9-127">RECOMMENDED: **"Customization"** allows you toochange hello "Contact your administrator" link toopoint tooa page or email address you define</span></span>

5. <span data-ttu-id="1bec9-128">선택 사항: hello **"Registration"** 화면 관리자에 대 한 hello 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-128">OPTIONAL: hello **"Registration"** screen provides administrators hello options for:</span></span>
    * <span data-ttu-id="1bec9-129">에 로그인 할 때 사용자가 tooregister 필요</span><span class="sxs-lookup"><span data-stu-id="1bec9-129">Require users tooregister when signing in</span></span>
    * <span data-ttu-id="1bec9-130">수 일 전에 사용자가 요청 tooreconfirm 해당 인증 정보</span><span class="sxs-lookup"><span data-stu-id="1bec9-130">Number of days before users are asked tooreconfirm their authentication information</span></span>

6. <span data-ttu-id="1bec9-131">선택 사항: hello **"알림"** 화면 hello 옵션을 관리자가 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-131">OPTIONAL: hello **"Notification"** screen provides administrators hello options to:</span></span>
    * <span data-ttu-id="1bec9-132">사용자에게 암호 재설정에 대해 알림</span><span class="sxs-lookup"><span data-stu-id="1bec9-132">Notify users on password resets</span></span>
    * <span data-ttu-id="1bec9-133">다른 관리자가 암호를 재설정하면 모든 관리자에게 알림</span><span class="sxs-lookup"><span data-stu-id="1bec9-133">Notify all admins when other admins reset their password</span></span>

<span data-ttu-id="1bec9-134">**현재는 Azure AD 테넌트에 SSPR을 구성했습니다**.</span><span class="sxs-lookup"><span data-stu-id="1bec9-134">**At this point, you have configured SSPR for your Azure AD tenant**.</span></span> <span data-ttu-id="1bec9-135">여기서 작업을 중지 하거나 tooconfigure 계속 수 암호 tooan의 동기화 온-프레미스 AD 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-135">You can stop here or continue on tooconfigure synchronization of passwords tooan on-premises AD domain.</span></span>

> [!NOTE]
> <span data-ttu-id="1bec9-136">관리자가 아닌 사용자로 SSPR을 테스트합니다. Microsoft가 Azure 관리자 유형 계정에 강력한 인증 요구 사항을 적용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-136">Test SSPR with a user and not an administrator as Microsoft enforces strong authentication requirements for Azure administrator type accounts.</span></span> <span data-ttu-id="1bec9-137">Hello 관리자 암호 정책에 대 한 자세한 내용은 참조는 [암호 정책 문서](active-directory-passwords-policy.md#administrator-password-policy-differences)합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-137">For more information regarding hello administrator password policy, see our [password policy article](active-directory-passwords-policy.md#administrator-password-policy-differences).</span></span>

## <a name="configure-synchronization-tooexisting-identity-source"></a><span data-ttu-id="1bec9-138">동기화 tooexisting id 소스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-138">Configure synchronization tooexisting identity source</span></span>

<span data-ttu-id="1bec9-139">tooenable 온-프레미스 AD identity 동기화 tooAzure, tooinstall 필요 하 고 구성할 [Azure AD Connect](./connect/active-directory-aadconnect.md) 조직에서 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-139">tooenable on-premises identity synchronization tooAzure AD, you need tooinstall and configure [Azure AD Connect](./connect/active-directory-aadconnect.md) on a server in your organization.</span></span> <span data-ttu-id="1bec9-140">이 응용 프로그램 동기화에서 사용자 및 그룹 기존 identity 소스 tooyour Azure AD 테 넌 트를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-140">This application handles synchronizing users and groups from your existing identity source tooyour Azure AD tenant.</span></span>

* [<span data-ttu-id="1bec9-141">AD Connect 디렉터리 동기화 또는 Azure AD Sync tooAzure에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="1bec9-141">Upgrade from DirSync or Azure AD Sync tooAzure AD Connect</span></span>](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [<span data-ttu-id="1bec9-142">기본 설정을 사용하여 Azure AD Connect 시작</span><span class="sxs-lookup"><span data-stu-id="1bec9-142">Getting started with Azure AD Connect using express settings</span></span>](./connect/active-directory-aadconnect-get-started-express.md)
* <span data-ttu-id="1bec9-143">[암호 쓰기 저장 구성](active-directory-passwords-writeback.md#configuring-password-writeback) Azure AD에서 toowrite 암호 tooyour 온-프레미스 디렉터리를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-143">[Configure password writeback](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite passwords from Azure AD back tooyour on-premises directory.</span></span>

## <a name="disabling-self-service-password-reset"></a><span data-ttu-id="1bec9-144">셀프 서비스 암호 재설정 해제</span><span class="sxs-lookup"><span data-stu-id="1bec9-144">Disabling self-service password reset</span></span>

<span data-ttu-id="1bec9-145">셀프 서비스 암호 재설정을 사용 하지 않도록 설정 하는 것은 Azure AD 테 넌 트를 열고 너무 것 처럼 간단할**암호 재설정 > 속성** > 선택 **None** 아래 **셀프 서비스 암호 재설정 사용 하도록 설정**</span><span class="sxs-lookup"><span data-stu-id="1bec9-145">Disabling self-service password reset is as simple as opening your Azure AD tenant and going too**Password Reset > Properties** > choose **None** under **Self Service Password Reset Enabled**</span></span>

### <a name="learn-more"></a><span data-ttu-id="1bec9-146">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1bec9-146">Learn more</span></span>
<span data-ttu-id="1bec9-147">링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-147">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="1bec9-148">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="1bec9-148">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="1bec9-149">[**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법</span><span class="sxs-lookup"><span data-stu-id="1bec9-149">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="1bec9-150">[**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자</span><span class="sxs-lookup"><span data-stu-id="1bec9-150">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="1bec9-151">[**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-151">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="1bec9-152">[**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정</span><span class="sxs-lookup"><span data-stu-id="1bec9-152">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="1bec9-153">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="1bec9-153">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="1bec9-154">[**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법</span><span class="sxs-lookup"><span data-stu-id="1bec9-154">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="1bec9-155">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="1bec9-155">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="1bec9-156">그 이유는</span><span class="sxs-lookup"><span data-stu-id="1bec9-156">Why?</span></span> <span data-ttu-id="1bec9-157">무엇을?</span><span class="sxs-lookup"><span data-stu-id="1bec9-157">What?</span></span> <span data-ttu-id="1bec9-158">어디서?</span><span class="sxs-lookup"><span data-stu-id="1bec9-158">Where?</span></span> <span data-ttu-id="1bec9-159">누가?</span><span class="sxs-lookup"><span data-stu-id="1bec9-159">Who?</span></span> <span data-ttu-id="1bec9-160">언제?</span><span class="sxs-lookup"><span data-stu-id="1bec9-160">When?</span></span> <span data-ttu-id="1bec9-161">-Tooask 항상 필요한 tooquestions 답변</span><span class="sxs-lookup"><span data-stu-id="1bec9-161">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="1bec9-162">[**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="1bec9-162">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bec9-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1bec9-163">Next steps</span></span>

<span data-ttu-id="1bec9-164">이 빠른 시작 사용자를 위해 tooconfigure 셀프 서비스 암호 재설정 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-164">In this quickstart, you’ve learned how tooconfigure self-service password reset for your users.</span></span> <span data-ttu-id="1bec9-165">다음이 단계를 수행 하는 Azure 포털 toocomplete toocontinue toohello hello toohello 포털 아래에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bec9-165">toocontinue toohello Azure portal toocomplete these steps follow hello link below toohello portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1bec9-166">셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="1bec9-166">Enable self-service password reset</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)


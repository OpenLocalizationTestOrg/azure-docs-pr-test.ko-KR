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
ms.openlocfilehash: 07c7f3ad066c735054cb339f6e09aa4d7d23f23a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a><span data-ttu-id="6e4c8-103">빠른 시작: Azure AD 셀프 서비스 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="6e4c8-103">Quickstart: Azure AD self-service password reset</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e4c8-104">**로그인하는 데 문제가 있나요?**</span><span class="sxs-lookup"><span data-stu-id="6e4c8-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="6e4c8-105">그렇다면 [암호를 변경하고 재설정하는 방법은 다음과 같습니다](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="6e4c8-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md).</span></span>

## <a name="rapidly-deploy-self-service-password-reset"></a><span data-ttu-id="6e4c8-106">신속하게 셀프 서비스 암호 재설정 배포</span><span class="sxs-lookup"><span data-stu-id="6e4c8-106">Rapidly deploy self-service password reset</span></span>

<span data-ttu-id="6e4c8-107">IT 관리자는 SSPR(셀프 서비스 암호 재설정)을 사용하여 사용자에게 자신의 암호 또는 계정을 재설정하거나 잠금 해제할 수 있는 권한을 간단하게 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-107">Self-service password reset (SSPR) offers a simple means for IT administrators to empower users to reset or unlock their passwords or accounts.</span></span> <span data-ttu-id="6e4c8-108">이 시스템에는 오용 또는 남용에 대해 경고하는 알림과 함께 사용자가 언제 시스템을 사용하는지 추적하는 구체적인 보고서가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-108">The system includes detailed reporting to track when users use the system along with notifications to alert you to misuse or abuse.</span></span>

<span data-ttu-id="6e4c8-109">이 가이드에서는 이미 여러분이 작업 평가판 또는 사용이 허가된 Azure AD 테넌트를 갖고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-109">This guide assumes you already have a working trial or licensed Azure AD tenant.</span></span> <span data-ttu-id="6e4c8-110">Azure AD 설정과 관련하여 도움이 필요한 경우 [Azure AD 시작하기](https://azure.microsoft.com/trial/get-started-active-directory/) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-110">If you need help setting up Azure AD, see the article [Getting Started with Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/).</span></span>

1. <span data-ttu-id="6e4c8-111">기존 Azure AD 테넌트에서 **"암호 재설정"**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-111">From your existing Azure AD tenant, select **"Password reset"**</span></span>

2. <span data-ttu-id="6e4c8-112">**"속성"** 화면의 "셀프 서비스 암호 재설정이 사용하도록 설정됨" 옵션에서 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-112">From the **"Properties"** screen, under the option "Self Service Password Reset Enabled" choose one of the following</span></span>
    * <span data-ttu-id="6e4c8-113">아무도 없음 - 아무도 SSPR 기능을 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="6e4c8-113">Nobody - No one is able to use SSPR functionality</span></span>
    * <span data-ttu-id="6e4c8-114">그룹 - 사용자가 선택하는 특정 Azure AD 그룹 구성원만 SSPR 기능을 사용할 수 있음</span><span class="sxs-lookup"><span data-stu-id="6e4c8-114">A group - Only members of a specific Azure AD group that you choose are able to use SSPR functionality</span></span>
    * <span data-ttu-id="6e4c8-115">모든 사람 - Azure AD 테넌트에 계정이 있는 모든 사용자가 SSPR 기능을 사용할 수 있음</span><span class="sxs-lookup"><span data-stu-id="6e4c8-115">Everybody - All users with accounts in your Azure AD tenant are able to use SSPR functionality</span></span>

3. <span data-ttu-id="6e4c8-116">**"인증 방법"** 화면에서 다음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-116">From the **"Authentication methods"** screen choose</span></span>
    * <span data-ttu-id="6e4c8-117">재설정에 필요한 방법 수 - 하나(최소) 또는 둘(최대)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-117">Number of methods required to reset - We support a minimum of one or a maximum of two</span></span>
    * <span data-ttu-id="6e4c8-118">사용자가 사용할 수 있는 방법 - 적어도 하나 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-118">Methods available to users - We need at least one but it never hurts to have an extra choice available</span></span>
        * <span data-ttu-id="6e4c8-119">**전자 메일**은 사용자가 구성한 인증 전자 메일 주소로 코드가 포함된 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-119">**Email** sends an email with a code to the user's configured authentication email address</span></span>
        * <span data-ttu-id="6e4c8-120">**휴대폰**은 사용자가 구성한 휴대폰 번호로 코드가 포함된 전화 또는 문자 메시지 중에 무엇을 받을 것인지 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-120">**Mobile Phone** gives the user the choice to receive a call or text with a code to their configured mobile phone number</span></span>
        * <span data-ttu-id="6e4c8-121">**사무실 전화**는 사용자가 구성한 사무실 전화 번호로 코드가 포함된 전화를 겁니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-121">**Office Phone** calls the user with a code to their configured office phone number</span></span>
        * <span data-ttu-id="6e4c8-122">**보안 질문**에서는 다음을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-122">**Security Questions** requires you to choose</span></span>
            * <span data-ttu-id="6e4c8-123">등록에 필요한 질문 수 - 성공적인 등록에 필요한 최소 수입니다. 즉, 사용자가 더 많이 대답하도록 선택하여 질문을 가져올 질문 풀을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-123">Number of questions required to register - The minimum for successful registration, meaning a user can choose to answer more to create a pool of questions to pull from.</span></span> <span data-ttu-id="6e4c8-124">이 옵션은 3-5로 설정해야 하며 재설정에 필요한 질문 수보다 많거나 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-124">This option can be set from 3-5 and must be greater than or equal to the number of questions required to reset.</span></span>
                * <span data-ttu-id="6e4c8-125">사용자 지정 질문은 보안 질문을 선택할 때 "사용자 지정" 단추를 클릭하여 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-125">Custom questions can be added by clicking the "Custom" button when selecting security questions</span></span>
            * <span data-ttu-id="6e4c8-126">재설정에 필요한 질문 수 - 사용자 암호를 재설정하거나 잠금 해제하도록 허용하기 전에 3-5개 질문에 대해 정확하게 대답하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-126">Number of questions required to reset - Can be set from 3-5 questions to be answered correctly before allowing a users password to be reset or unlocked.</span></span>

4. <span data-ttu-id="6e4c8-127">권장 사항: **"사용자 지정"**을 사용하여 "관리자에게 문의" 링크가 사용자가 정의한 페이지 또는 전자 메일 주소를 가리키도록 변경할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="6e4c8-127">RECOMMENDED: **"Customization"** allows you to change the "Contact your administrator" link to point to a page or email address you define</span></span>

5. <span data-ttu-id="6e4c8-128">선택 사항: **"등록"** 화면은 관리자에게 다음 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-128">OPTIONAL: The **"Registration"** screen provides administrators the options for:</span></span>
    * <span data-ttu-id="6e4c8-129">로그인 시 사용자가 등록하도록 요구</span><span class="sxs-lookup"><span data-stu-id="6e4c8-129">Require users to register when signing in</span></span>
    * <span data-ttu-id="6e4c8-130">사용자가 인증 정보를 다시 확인해야 하기 전의 일 수</span><span class="sxs-lookup"><span data-stu-id="6e4c8-130">Number of days before users are asked to reconfirm their authentication information</span></span>

6. <span data-ttu-id="6e4c8-131">선택 사항: **"알림"** 화면에서 관리자에게 제공되는 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-131">OPTIONAL: The **"Notification"** screen provides administrators the options to:</span></span>
    * <span data-ttu-id="6e4c8-132">사용자에게 암호 재설정에 대해 알림</span><span class="sxs-lookup"><span data-stu-id="6e4c8-132">Notify users on password resets</span></span>
    * <span data-ttu-id="6e4c8-133">다른 관리자가 암호를 재설정하면 모든 관리자에게 알림</span><span class="sxs-lookup"><span data-stu-id="6e4c8-133">Notify all admins when other admins reset their password</span></span>

<span data-ttu-id="6e4c8-134">**현재는 Azure AD 테넌트에 SSPR을 구성했습니다**.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-134">**At this point, you have configured SSPR for your Azure AD tenant**.</span></span> <span data-ttu-id="6e4c8-135">여기서 그만 해도 되고 계속해서 온-프레미스 AD 도메인에 암호 동기화를 구성해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-135">You can stop here or continue on to configure synchronization of passwords to an on-premises AD domain.</span></span>

> [!NOTE]
> <span data-ttu-id="6e4c8-136">관리자가 아닌 사용자로 SSPR을 테스트합니다. Microsoft가 Azure 관리자 유형 계정에 강력한 인증 요구 사항을 적용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-136">Test SSPR with a user and not an administrator as Microsoft enforces strong authentication requirements for Azure administrator type accounts.</span></span> <span data-ttu-id="6e4c8-137">관리자 암호 정책에 대한 자세한 내용은 [암호 정책 문서](active-directory-passwords-policy.md#administrator-password-policy-differences)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-137">For more information regarding the administrator password policy, see our [password policy article](active-directory-passwords-policy.md#administrator-password-policy-differences).</span></span>

## <a name="configure-synchronization-to-existing-identity-source"></a><span data-ttu-id="6e4c8-138">기존 ID 소스에 동기화 구성</span><span class="sxs-lookup"><span data-stu-id="6e4c8-138">Configure synchronization to existing identity source</span></span>

<span data-ttu-id="6e4c8-139">Azure AD에 온-프레미스 ID 동기화를 사용하려면 조직의 서버에 [Azure AD Connect](./connect/active-directory-aadconnect.md)를 설치하고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-139">To enable on-premises identity synchronization to Azure AD, you need to install and configure [Azure AD Connect](./connect/active-directory-aadconnect.md) on a server in your organization.</span></span> <span data-ttu-id="6e4c8-140">이 응용 프로그램은 사용자 및 그룹을 기존 ID 원본에서 Azure AD 테넌트로 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-140">This application handles synchronizing users and groups from your existing identity source to your Azure AD tenant.</span></span>

* [<span data-ttu-id="6e4c8-141">DirSync 또는 Azure AD Sync에서 Azure AD Connect로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="6e4c8-141">Upgrade from DirSync or Azure AD Sync to Azure AD Connect</span></span>](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [<span data-ttu-id="6e4c8-142">기본 설정을 사용하여 Azure AD Connect 시작</span><span class="sxs-lookup"><span data-stu-id="6e4c8-142">Getting started with Azure AD Connect using express settings</span></span>](./connect/active-directory-aadconnect-get-started-express.md)
* <span data-ttu-id="6e4c8-143">[비밀번호 쓰기 저장을 구성](active-directory-passwords-writeback.md#configuring-password-writeback)하여 Azure AD에서 온-프레미스 디렉터리로 비밀번호 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="6e4c8-143">[Configure password writeback](active-directory-passwords-writeback.md#configuring-password-writeback) to write passwords from Azure AD back to your on-premises directory.</span></span>

## <a name="disabling-self-service-password-reset"></a><span data-ttu-id="6e4c8-144">셀프 서비스 암호 재설정 해제</span><span class="sxs-lookup"><span data-stu-id="6e4c8-144">Disabling self-service password reset</span></span>

<span data-ttu-id="6e4c8-145">셀프 서비스 암호 재설정을 사용하지 않도록 설정하려면 Azure AD 테넌트를 열고 **암호 재설정 > 속성**으로 이동하여 **셀프 서비스 암호 재설정이 사용하도록 설정됨** 아래에서 **아무도 없음**을 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-145">Disabling self-service password reset is as simple as opening your Azure AD tenant and going to **Password Reset > Properties** > choose **None** under **Self Service Password Reset Enabled**</span></span>

### <a name="learn-more"></a><span data-ttu-id="6e4c8-146">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="6e4c8-146">Learn more</span></span>
<span data-ttu-id="6e4c8-147">다음 링크는 Azure AD를 사용한 암호 재설정에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-147">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="6e4c8-148">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="6e4c8-148">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="6e4c8-149">[**데이터**](active-directory-passwords-data.md) - 암호 관리에 필요한 데이터 및 사용 방식을 이해</span><span class="sxs-lookup"><span data-stu-id="6e4c8-149">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="6e4c8-150">[**롤아웃**](active-directory-passwords-best-practices.md) - 여기서 제공하는 지침을 사용하여 배포 계획을 세우고 사용자에게 SSPR 배포</span><span class="sxs-lookup"><span data-stu-id="6e4c8-150">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="6e4c8-151">[**사용자 지정**](active-directory-passwords-customize.md) - 회사 SSPR 경험의 모양과 느낌을 사용자 지정.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-151">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="6e4c8-152">[**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정</span><span class="sxs-lookup"><span data-stu-id="6e4c8-152">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="6e4c8-153">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="6e4c8-153">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="6e4c8-154">[**기술 심층 분석**](active-directory-passwords-how-it-works.md) - 작동 방식을 이해하기 위해 심층 분석</span><span class="sxs-lookup"><span data-stu-id="6e4c8-154">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="6e4c8-155">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="6e4c8-155">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="6e4c8-156">그 이유는</span><span class="sxs-lookup"><span data-stu-id="6e4c8-156">Why?</span></span> <span data-ttu-id="6e4c8-157">무엇을?</span><span class="sxs-lookup"><span data-stu-id="6e4c8-157">What?</span></span> <span data-ttu-id="6e4c8-158">어디서?</span><span class="sxs-lookup"><span data-stu-id="6e4c8-158">Where?</span></span> <span data-ttu-id="6e4c8-159">누가?</span><span class="sxs-lookup"><span data-stu-id="6e4c8-159">Who?</span></span> <span data-ttu-id="6e4c8-160">언제?</span><span class="sxs-lookup"><span data-stu-id="6e4c8-160">When?</span></span> <span data-ttu-id="6e4c8-161">- 많은 분들이 항상 묻는 질문에 대한 답변입니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-161">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="6e4c8-162">[**문제 해결**](active-directory-passwords-troubleshoot.md) - SSPR의 일반적인 문제 해결 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="6e4c8-162">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e4c8-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6e4c8-163">Next steps</span></span>

<span data-ttu-id="6e4c8-164">이 퀵스타트에서는 사용자를 위한 셀프 서비스 암호 재설정 구성 방법을 알게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-164">In this quickstart, you’ve learned how to configure self-service password reset for your users.</span></span> <span data-ttu-id="6e4c8-165">이 단계를 완료하기 위해 Azure Portal로 진행하려면 아래 포털 링크를 따라 가십시오.</span><span class="sxs-lookup"><span data-stu-id="6e4c8-165">To continue to the Azure portal to complete these steps follow the link below to the portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6e4c8-166">셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="6e4c8-166">Enable self-service password reset</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)


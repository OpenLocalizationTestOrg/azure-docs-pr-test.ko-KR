---
title: "롤아웃: Azure AD SSPR | Microsoft 문서"
description: "Azure AD 셀프 서비스 암호 재설정을 성공적으로 롤아웃하기 위한 팁"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: daa5f9f6a4c9cf5eb20ffe02368444682c0ccb42
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="roll-out-password-reset-for-users"></a><span data-ttu-id="e0120-103">사용자 암호 재설정 롤아웃</span><span class="sxs-lookup"><span data-stu-id="e0120-103">Roll out password reset for users</span></span>

<span data-ttu-id="e0120-104">대부분의 고객은 SSPR 기능의 원활한 롤아웃을 위해 수반되는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-104">Most customers follow the steps that follow to ensure a smooth rollout of SSPR functionality.</span></span>

1. [<span data-ttu-id="e0120-105">디렉터리에서 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="e0120-105">Enable password reset in your directory</span></span>](active-directory-passwords-getting-started.md)
2. [<span data-ttu-id="e0120-106">비밀번호 쓰기 저장을 위한 온-프레미스 AD 권한 구성</span><span class="sxs-lookup"><span data-stu-id="e0120-106">Configure on-premises AD permissions for password writeback</span></span>](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. <span data-ttu-id="e0120-107">[비밀번호 쓰기 저장을 구성](active-directory-passwords-writeback.md#configuring-password-writeback)하여 Azure AD에서 온-프레미스 디렉터리로 비밀번호를 다시 기록합니다</span><span class="sxs-lookup"><span data-stu-id="e0120-107">[Configure password writeback](active-directory-passwords-writeback.md#configuring-password-writeback) to write passwords from Azure AD back to your on-premises directory</span></span>
4. [<span data-ttu-id="e0120-108">필요한 라이선스 할당 및 확인</span><span class="sxs-lookup"><span data-stu-id="e0120-108">Assign and verify required licenses</span></span>](active-directory-passwords-licensing.md)
5. <span data-ttu-id="e0120-109">점진적으로 롤아웃하려는 경우 암호 재설정을 사용자 그룹으로 제한하여 시간에 따라 기능을 천천히 롤아웃할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-109">If you want to roll out gradually, you can optionally limit password reset to a group of users to roll out the feature slowly over time.</span></span> <span data-ttu-id="e0120-110">이렇게 하려면**셀프 서비스 암호 재설정이 사용하도록 설정됨**을 **모든 사람**에서 **그룹**으로 전환하고 암호 재설정을 사용할 보안 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-110">To do this set the **Self Service Password Reset Enabled** toggle from **Everybody** to **A group** and select a security group to enable for password reset.</span></span> <span data-ttu-id="e0120-111">이 그룹의 모든 구성원에게 라이선스가 할당되어 있어야 하며 [그룹 기반 라이선스](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing)를 사용하는 훌륭한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-111">The members of this group must all have licenses assigned to them and is a great way to enable [Group Based Licensing](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).</span></span>
6. <span data-ttu-id="e0120-112">정책에 따라 최소 [인증 데이터](active-directory-passwords-data.md) 집합을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-112">Populate the minimum set of [Authentication Data](active-directory-passwords-data.md), based on your policy.</span></span>
7. <span data-ttu-id="e0120-113">사용자에게 등록 방법 및 재설정 방법을 보여 주는 지침을 제공하여 SSPR 사용 방법을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-113">Teach your users how to use SSPR, by sending them instructions to show them how to register and how to reset.</span></span>
    > [!NOTE]
    > <span data-ttu-id="e0120-114">관리자가 아닌 사용자로 SSPR을 테스트합니다. Microsoft가 Azure 관리자 유형 계정에 강력한 인증 요구 사항을 적용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-114">Test SSPR with a user and not an administrator as Microsoft enforces strong authentication requirements for Azure administrator type accounts.</span></span> <span data-ttu-id="e0120-115">관리자 암호 정책에 대한 자세한 내용은 [심층 분석 문서](active-directory-passwords-how-it-works.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0120-115">For more information regarding the administrator password policy, see our [deep dive article](active-directory-passwords-how-it-works.md).</span></span>

8. <span data-ttu-id="e0120-116">언제든지 등록을 적용할 수 있으며, 일정 기간이 지나면 인증 정보를 다시 확인하도록 사용자에게 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-116">You can choose to enforce registration at any point, and require users to reconfirm their authentication information after a certain period of time.</span></span> <span data-ttu-id="e0120-117">사용자가 의무적으로 등록하지 않아도 되게 하려면 [최종 사용자에게 등록을 요구하지 않고 암호 재설정을 배포](active-directory-passwords-data.md)하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-117">If you don't want your users to have to register, you can [deploy password reset without requiring end-user registration](active-directory-passwords-data.md).</span></span>
9. <span data-ttu-id="e0120-118">시간이 지나면 [Azure AD에서 제공하는 보고서](active-directory-passwords-reporting.md)를 검토하여 사용자의 등록과 사용을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-118">Over time, review users registering and using by viewing the [reporting provided by Azure AD](active-directory-passwords-reporting.md).</span></span>

## <a name="email-based-rollout"></a><span data-ttu-id="e0120-119">전자 메일 기반 롤아웃</span><span class="sxs-lookup"><span data-stu-id="e0120-119">Email-based rollout</span></span>

<span data-ttu-id="e0120-120">사용자가 SSPR을 사용하게 만드는 가장 쉬운 방법은 간단한 지침이 포함된 전자 메일 캠페인이라는 사실을 많은 고객이 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-120">Many customers find an email campaign, with simple to use instructions, is the easiest way to get users to use SSPR.</span></span> [<span data-ttu-id="e0120-121">Microsoft는 고객의 롤아웃에 도움이 되도록 템플릿으로 사용할 수 있는 세 가지 간단한 전자 메일을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-121">We have created three simple emails that you can use as templates to help in your rollout.</span></span>](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* <span data-ttu-id="e0120-122">**출시 예정** 전자 메일 템플릿 - 롤아웃 몇 주 또는 며칠 전에 사용자에게 어떤 작업을 수행해야 한다는 사실을 알리기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-122">**Coming Soon** email template to be used in the weeks or days before rollout to let users know they need to do something.</span></span>
* <span data-ttu-id="e0120-123">**현재 사용 가능한** 전자 메일 템플릿 - 사용자가 필요할 때 SSPR을 사용할 수 있도록 출시 당일에 사용자가 인증 데이터를 등록하고 확인하도록 유도하기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-123">**Available Now** email template to be used the day of launch to drive users to register and confirm their authentication data so they can use SSPR when they need it.</span></span>
* <span data-ttu-id="e0120-124">**등록 미리 알림** 전자 메일 템플릿 - 배포 며칠 후 또는 몇 주 후에 사용자에게 인증 데이터를 등록하고 확인하라고 알리기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-124">**Sign up Reminder** email template for a few days to weeks after deployment to remind users to register and confirm their authentication data.</span></span>

## <a name="creating-your-own-password-portal"></a><span data-ttu-id="e0120-125">고유의 암호 포털 만들기</span><span class="sxs-lookup"><span data-stu-id="e0120-125">Creating your own password portal</span></span>

<span data-ttu-id="e0120-126">대부분의 대기업 고객은 웹 페이지를 호스팅하고 https://passwords.contoso.com 같은 루트 DNS 항목을 만드는 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-126">Many of our larger customers choose to host webpage and create a root DNS entry, like https://passwords.contoso.com.</span></span> <span data-ttu-id="e0120-127">고객은 이 페이지를 Azure AD 암호 재설정, 암호 재설정 등록, 암호 변경 포털 및 기타 조직 관련 정보의 링크로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-127">They populate this page with links to the Azure AD password reset, password reset registration, password change portals, and other organization-specific information.</span></span> <span data-ttu-id="e0120-128">이러한 방식으로 보내는 전자 메일 통신 또는 전단지에서, 사용자가 서비스를 사용해야 할 때 이동할 수 있는 유명하고 기억하기 쉬운 URL을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-128">In any email communications or fliers, you send out, you can then include a branded, memorable, URL that users can go to when they need to use the services.</span></span>

* <span data-ttu-id="e0120-129">암호 재설정 포털 - https://passwordreset.microsoftonline.com/</span><span class="sxs-lookup"><span data-stu-id="e0120-129">Password reset portal - https://passwordreset.microsoftonline.com/</span></span>
* <span data-ttu-id="e0120-130">암호 재설정 등록 포털 - http://aka.ms/ssprsetup</span><span class="sxs-lookup"><span data-stu-id="e0120-130">Password reset registration portal - http://aka.ms/ssprsetup</span></span>
* <span data-ttu-id="e0120-131">암호 변경 포털 - https://account.activedirectory.windowsazure.com/ChangePassword.aspx</span><span class="sxs-lookup"><span data-stu-id="e0120-131">Password change portal - https://account.activedirectory.windowsazure.com/ChangePassword.aspx</span></span>

## <a name="using-enforced-registration"></a><span data-ttu-id="e0120-132">강제 등록 사용</span><span class="sxs-lookup"><span data-stu-id="e0120-132">Using enforced registration</span></span>

<span data-ttu-id="e0120-133">사용자가 암호 재설정을 등록하게 하려면 사용자가 Azure AD를 사용하여 로그인할 때 강제로 등록하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-133">If you want your users to register for password reset, you can force them to register when they sign in using Azure AD.</span></span> <span data-ttu-id="e0120-134">**등록** 탭의 **로그인할 때 사용자가 등록해야 함** 옵션을 사용하여 디렉터리의 **암호 재설정** 블레이드에서 이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-134">You can enable this option from your directory’s **Password reset** blade by enabling the **Require Users to Register when Signing in** option on the **Registration** tab.</span></span>

<span data-ttu-id="e0120-135">관리자는 **사용자가 인증 정보를 다시 확인해야 할 때까지 남은 일 수**를 0-730일 사이로 설정하여 일정 기간 후 사용자가 다시 등록하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-135">Administrators can require users to re-register after a period of time by setting the **Number of days before users are asked to reconfirm their authentication information** between 0-730 days.</span></span>

<span data-ttu-id="e0120-136">이 옵션을 설정한 다음 사용자가 로그인하면 사용자의 요청에 따라 인증 정보를 확인해야 한다는 내용의 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-136">After you enable this option, users signing will see a message that informs them their administrator has required them to verify their authentication information.</span></span>

## <a name="populate-authentication-data"></a><span data-ttu-id="e0120-137">인증 데이터 채우기</span><span class="sxs-lookup"><span data-stu-id="e0120-137">Populate authentication data</span></span>

<span data-ttu-id="e0120-138">[사용자의 인증 데이터를 채우면](active-directory-passwords-data.md) 사용자가 암호 재설정을 등록하지 않아도 SSPR을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-138">If you [populate authentication data for your users](active-directory-passwords-data.md), then users do not need to register for password reset before being able to use SSPR.</span></span> <span data-ttu-id="e0120-139">관리자가 정의한 암호 재설정 정책을 충족하는 인증 데이터가 정의되어 있는 한, 사용자는 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-139">As long as users have the authentication data defined that meets the password reset policy you have defined, users are able to reset their passwords.</span></span>

## <a name="disabling-self-service-password-reset"></a><span data-ttu-id="e0120-140">셀프 서비스 암호 재설정 해제</span><span class="sxs-lookup"><span data-stu-id="e0120-140">Disabling self-service password reset</span></span>

<span data-ttu-id="e0120-141">셀프 서비스 암호 재설정을 해제하는 방법은 아주 간단합니다. Azure AD 테넌트를 열고, **암호 재설정**, **속성**으로 이동하여 **셀프 서비스 암호 재설정이 사용하도록 설정됨** 아래에서 **아무도 없음**을 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-141">Disabling self-service password reset is as simple as opening your Azure AD tenant and going to **Password Reset**, **Properties**, and choosing **Nobody** under **Self Service Password Reset Enabled**</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0120-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0120-142">Next steps</span></span>

<span data-ttu-id="e0120-143">다음 링크는 Azure AD를 사용한 암호 재설정에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-143">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="e0120-144">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="e0120-144">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="e0120-145">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="e0120-145">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="e0120-146">[**데이터**](active-directory-passwords-data.md) - 암호 관리에 필요한 데이터 및 사용 방식을 이해</span><span class="sxs-lookup"><span data-stu-id="e0120-146">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="e0120-147">[**사용자 지정**](active-directory-passwords-customize.md) - 회사 SSPR 경험의 모양과 느낌을 사용자 지정.</span><span class="sxs-lookup"><span data-stu-id="e0120-147">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="e0120-148">[**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정</span><span class="sxs-lookup"><span data-stu-id="e0120-148">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="e0120-149">[**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리</span><span class="sxs-lookup"><span data-stu-id="e0120-149">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="e0120-150">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="e0120-150">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="e0120-151">[**기술 심층 분석**](active-directory-passwords-how-it-works.md) - 작동 방식을 이해하기 위해 심층 분석</span><span class="sxs-lookup"><span data-stu-id="e0120-151">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="e0120-152">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="e0120-152">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="e0120-153">그 이유는</span><span class="sxs-lookup"><span data-stu-id="e0120-153">Why?</span></span> <span data-ttu-id="e0120-154">무엇을?</span><span class="sxs-lookup"><span data-stu-id="e0120-154">What?</span></span> <span data-ttu-id="e0120-155">어디서?</span><span class="sxs-lookup"><span data-stu-id="e0120-155">Where?</span></span> <span data-ttu-id="e0120-156">누가?</span><span class="sxs-lookup"><span data-stu-id="e0120-156">Who?</span></span> <span data-ttu-id="e0120-157">언제?</span><span class="sxs-lookup"><span data-stu-id="e0120-157">When?</span></span> <span data-ttu-id="e0120-158">- 많은 분들이 항상 묻는 질문에 대한 답변입니다.</span><span class="sxs-lookup"><span data-stu-id="e0120-158">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="e0120-159">[**문제 해결**](active-directory-passwords-troubleshoot.md) - SSPR의 일반적인 문제 해결 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="e0120-159">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
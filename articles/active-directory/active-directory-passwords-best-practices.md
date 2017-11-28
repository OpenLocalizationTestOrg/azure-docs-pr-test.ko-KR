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
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a><span data-ttu-id="8f2ac-103">사용자 암호 재설정 롤아웃</span><span class="sxs-lookup"><span data-stu-id="8f2ac-103">Roll out password reset for users</span></span>

<span data-ttu-id="8f2ac-104">대부분의 고객이 tooensure SSPR 기능 공개를 수행 하는 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-104">Most customers follow hello steps that follow tooensure a smooth rollout of SSPR functionality.</span></span>

1. [<span data-ttu-id="8f2ac-105">디렉터리에서 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="8f2ac-105">Enable password reset in your directory</span></span>](active-directory-passwords-getting-started.md)
2. [<span data-ttu-id="8f2ac-106">비밀번호 쓰기 저장을 위한 온-프레미스 AD 권한 구성</span><span class="sxs-lookup"><span data-stu-id="8f2ac-106">Configure on-premises AD permissions for password writeback</span></span>](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. <span data-ttu-id="8f2ac-107">[암호 쓰기 저장 구성](active-directory-passwords-writeback.md#configuring-password-writeback) Azure AD에서 toowrite 암호 tooyour 온-프레미스 디렉터리 백업</span><span class="sxs-lookup"><span data-stu-id="8f2ac-107">[Configure password writeback](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite passwords from Azure AD back tooyour on-premises directory</span></span>
4. [<span data-ttu-id="8f2ac-108">필요한 라이선스 할당 및 확인</span><span class="sxs-lookup"><span data-stu-id="8f2ac-108">Assign and verify required licenses</span></span>](active-directory-passwords-licensing.md)
5. <span data-ttu-id="8f2ac-109">Tooroll 있습니다 점차적으로 아웃 하려는 경우 필요에 따라 제한 암호 다시 설정할 수 tooa 그룹 사용자 tooroll hello 기능을 천천히 시간이 지남에 따라.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-109">If you want tooroll out gradually, you can optionally limit password reset tooa group of users tooroll out hello feature slowly over time.</span></span> <span data-ttu-id="8f2ac-110">toodo이 값은 설정 hello **셀프 서비스 암호 재설정 활성화** 에서 설정/해제 **모든 사용자에 게** 너무**그룹** 하 고 암호 재설정에 대 한 보안 그룹 tooenable를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-110">toodo this set hello **Self Service Password Reset Enabled** toggle from **Everybody** too**A group** and select a security group tooenable for password reset.</span></span> <span data-ttu-id="8f2ac-111">hello이 그룹의 구성원 라이선스가 할당 toothem 있어야 이며 좋은 방법 tooenable [그룹 기반 라이선스](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-111">hello members of this group must all have licenses assigned toothem and is a great way tooenable [Group Based Licensing](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).</span></span>
6. <span data-ttu-id="8f2ac-112">Hello 최소 집합을 채우는 [인증 데이터](active-directory-passwords-data.md)정책에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-112">Populate hello minimum set of [Authentication Data](active-directory-passwords-data.md), based on your policy.</span></span>
7. <span data-ttu-id="8f2ac-113">사용자가 어떻게 설명 지침 tooshow 보내 toouse SSPR에 어떻게 tooregister와 방법을 tooreset 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-113">Teach your users how toouse SSPR, by sending them instructions tooshow them how tooregister and how tooreset.</span></span>
    > [!NOTE]
    > <span data-ttu-id="8f2ac-114">관리자가 아닌 사용자로 SSPR을 테스트합니다. Microsoft가 Azure 관리자 유형 계정에 강력한 인증 요구 사항을 적용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-114">Test SSPR with a user and not an administrator as Microsoft enforces strong authentication requirements for Azure administrator type accounts.</span></span> <span data-ttu-id="8f2ac-115">Hello 관리자 암호 정책에 대 한 자세한 내용은 참조는 [심층 분석 문서](active-directory-passwords-how-it-works.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-115">For more information regarding hello administrator password policy, see our [deep dive article](active-directory-passwords-how-it-works.md).</span></span>

8. <span data-ttu-id="8f2ac-116">언제 든 지 tooenforce 등록을 선택할 수 있으며 사용자 tooreconfirm 일정 기간 후 해당 인증 정보를 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-116">You can choose tooenforce registration at any point, and require users tooreconfirm their authentication information after a certain period of time.</span></span> <span data-ttu-id="8f2ac-117">사용자가 toohave tooregister 사용 하지 않으려는 경우 다음을 할 수 있습니다 [암호 재설정 최종 사용자 등록 필요 없이 배포](active-directory-passwords-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-117">If you don't want your users toohave tooregister, you can [deploy password reset without requiring end-user registration](active-directory-passwords-data.md).</span></span>
9. <span data-ttu-id="8f2ac-118">시간이 지남에 따라 등록 하 고 hello를 확인 하 여 사용 하 여 사용자가 검토 [Azure AD에서 제공 보고](active-directory-passwords-reporting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-118">Over time, review users registering and using by viewing hello [reporting provided by Azure AD](active-directory-passwords-reporting.md).</span></span>

## <a name="email-based-rollout"></a><span data-ttu-id="8f2ac-119">전자 메일 기반 롤아웃</span><span class="sxs-lookup"><span data-stu-id="8f2ac-119">Email-based rollout</span></span>

<span data-ttu-id="8f2ac-120">많은 고객 간단한 toouse 지침이 포함 된 전자 메일 캠페인 hello 가장 쉬운 방법은 tooget 사용자 toouse SSPR을 찾을 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-120">Many customers find an email campaign, with simple toouse instructions, is hello easiest way tooget users toouse SSPR.</span></span> [<span data-ttu-id="8f2ac-121">롤아웃의 템플릿 toohelp으로 사용할 수 있는 세 개의 간단한 전자 메일을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-121">We have created three simple emails that you can use as templates toohelp in your rollout.</span></span>](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* <span data-ttu-id="8f2ac-122">**곧 출시 됩니다** 템플릿 toobe hello 주 또는 어떤 toodo 필요한 롤아웃 toolet 사용자가 알고 전 까지의 일에 사용 되는 전자 메일입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-122">**Coming Soon** email template toobe used in hello weeks or days before rollout toolet users know they need toodo something.</span></span>
* <span data-ttu-id="8f2ac-123">**지금 사용 가능** 시작 toodrive 사용자 tooregister 요일을 사용 toobe hello 서식 파일을 전자 메일 및 SSPR 필요할 때 사용할 수 있도록가 인증 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-123">**Available Now** email template toobe used hello day of launch toodrive users tooregister and confirm their authentication data so they can use SSPR when they need it.</span></span>
* <span data-ttu-id="8f2ac-124">**미리 알림 등록** 몇 일 tooweeks에 대 한 템플릿 배포 tooremind 사용자 tooregister 후 전자 메일 및가 인증 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-124">**Sign up Reminder** email template for a few days tooweeks after deployment tooremind users tooregister and confirm their authentication data.</span></span>

## <a name="creating-your-own-password-portal"></a><span data-ttu-id="8f2ac-125">고유의 암호 포털 만들기</span><span class="sxs-lookup"><span data-stu-id="8f2ac-125">Creating your own password portal</span></span>

<span data-ttu-id="8f2ac-126">대부분의 큰 고객 toohost 웹 페이지를 선택 하 고 루트 https://passwords.contoso.com 같은 DNS 항목을 만듭니다. 링크 toohello Azure AD 암호 재설정에이 페이지를 채우는, 암호 재설정 등록, 암호 변경 포털 및 기타 조직 관련 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-126">Many of our larger customers choose toohost webpage and create a root DNS entry, like https://passwords.contoso.com. They populate this page with links toohello Azure AD password reset, password reset registration, password change portals, and other organization-specific information.</span></span> <span data-ttu-id="8f2ac-127">모든 전자 메일 통신 또는 전단지에 보낸를 포함할 수 있습니다는 브랜드가 지정 된 기억 하기 쉬운, URL toowhen toouse hello 서비스 필요한 사용자가 처리할 수 있다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-127">In any email communications or fliers, you send out, you can then include a branded, memorable, URL that users can go toowhen they need toouse hello services.</span></span>

* <span data-ttu-id="8f2ac-128">암호 재설정 포털 - https://passwordreset.microsoftonline.com/</span><span class="sxs-lookup"><span data-stu-id="8f2ac-128">Password reset portal - https://passwordreset.microsoftonline.com/</span></span>
* <span data-ttu-id="8f2ac-129">암호 재설정 등록 포털 - http://aka.ms/ssprsetup</span><span class="sxs-lookup"><span data-stu-id="8f2ac-129">Password reset registration portal - http://aka.ms/ssprsetup</span></span>
* <span data-ttu-id="8f2ac-130">암호 변경 포털 - https://account.activedirectory.windowsazure.com/ChangePassword.aspx</span><span class="sxs-lookup"><span data-stu-id="8f2ac-130">Password change portal - https://account.activedirectory.windowsazure.com/ChangePassword.aspx</span></span>

## <a name="using-enforced-registration"></a><span data-ttu-id="8f2ac-131">강제 등록 사용</span><span class="sxs-lookup"><span data-stu-id="8f2ac-131">Using enforced registration</span></span>

<span data-ttu-id="8f2ac-132">암호 재설정을 위해 사용자가 tooregister를 원하는 Azure AD를 사용 하 여 로그인 할 때 해당를 tooregister를 강제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-132">If you want your users tooregister for password reset, you can force them tooregister when they sign in using Azure AD.</span></span> <span data-ttu-id="8f2ac-133">사용자 디렉터리에서이 옵션을 사용할 수 있습니다 **암호 재설정** hello를 사용 하 여 블레이드 **에 로그인 할 때 사용자가 필요한 tooRegister** hello에 대 한 옵션 **등록** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-133">You can enable this option from your directory’s **Password reset** blade by enabling hello **Require Users tooRegister when Signing in** option on hello **Registration** tab.</span></span>

<span data-ttu-id="8f2ac-134">관리자 hello 설정 하 여 시간이 지나면 사용자 toore 레지스터에 요구할 수 있습니다 **수가 일 전에 사용자가 요청 tooreconfirm 해당 인증 정보** 0-730 사이의 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-134">Administrators can require users toore-register after a period of time by setting hello **Number of days before users are asked tooreconfirm their authentication information** between 0-730 days.</span></span>

<span data-ttu-id="8f2ac-135">서명 하는 사용자가 해당 관리자가 tooverify 요청을 알려 주는 메시지가 표시 됩니다이 옵션을 사용 하도록 설정한 후 해당 인증 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-135">After you enable this option, users signing will see a message that informs them their administrator has required them tooverify their authentication information.</span></span>

## <a name="populate-authentication-data"></a><span data-ttu-id="8f2ac-136">인증 데이터 채우기</span><span class="sxs-lookup"><span data-stu-id="8f2ac-136">Populate authentication data</span></span>

<span data-ttu-id="8f2ac-137">경우 있습니다 [사용자에 대 한 인증 데이터를 채우려면](active-directory-passwords-data.md), 사용자가 암호 재설정 수 toouse SSPR에 대 한 tooregister 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-137">If you [populate authentication data for your users](active-directory-passwords-data.md), then users do not need tooregister for password reset before being able toouse SSPR.</span></span> <span data-ttu-id="8f2ac-138">사용자가 수 tooreset hello 인증 정의 맞는 데이터 hello 암호 재설정 정책을 정의한를 보유 하는 사용자, 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-138">As long as users have hello authentication data defined that meets hello password reset policy you have defined, users are able tooreset their passwords.</span></span>

## <a name="disabling-self-service-password-reset"></a><span data-ttu-id="8f2ac-139">셀프 서비스 암호 재설정 해제</span><span class="sxs-lookup"><span data-stu-id="8f2ac-139">Disabling self-service password reset</span></span>

<span data-ttu-id="8f2ac-140">셀프 서비스 암호 재설정을 사용 하지 않도록 설정 하는 것은 Azure AD 테 넌 트를 열고 너무 것 처럼 간단할**암호 재설정**, **속성**를 선택 하 고 **아무도** 아래 **셀프 서비스 암호 재설정을 사용 하도록 설정**</span><span class="sxs-lookup"><span data-stu-id="8f2ac-140">Disabling self-service password reset is as simple as opening your Azure AD tenant and going too**Password Reset**, **Properties**, and choosing **Nobody** under **Self Service Password Reset Enabled**</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f2ac-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f2ac-141">Next steps</span></span>

<span data-ttu-id="8f2ac-142">링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-142">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="8f2ac-143">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="8f2ac-143">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="8f2ac-144">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="8f2ac-144">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="8f2ac-145">[**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법</span><span class="sxs-lookup"><span data-stu-id="8f2ac-145">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="8f2ac-146">[**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2ac-146">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="8f2ac-147">[**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정</span><span class="sxs-lookup"><span data-stu-id="8f2ac-147">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="8f2ac-148">[**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리</span><span class="sxs-lookup"><span data-stu-id="8f2ac-148">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="8f2ac-149">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="8f2ac-149">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="8f2ac-150">[**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법</span><span class="sxs-lookup"><span data-stu-id="8f2ac-150">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="8f2ac-151">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="8f2ac-151">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="8f2ac-152">그 이유는</span><span class="sxs-lookup"><span data-stu-id="8f2ac-152">Why?</span></span> <span data-ttu-id="8f2ac-153">무엇을?</span><span class="sxs-lookup"><span data-stu-id="8f2ac-153">What?</span></span> <span data-ttu-id="8f2ac-154">어디서?</span><span class="sxs-lookup"><span data-stu-id="8f2ac-154">Where?</span></span> <span data-ttu-id="8f2ac-155">누가?</span><span class="sxs-lookup"><span data-stu-id="8f2ac-155">Who?</span></span> <span data-ttu-id="8f2ac-156">언제?</span><span class="sxs-lookup"><span data-stu-id="8f2ac-156">When?</span></span> <span data-ttu-id="8f2ac-157">-Tooask 항상 필요한 tooquestions 답변</span><span class="sxs-lookup"><span data-stu-id="8f2ac-157">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="8f2ac-158">[**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="8f2ac-158">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

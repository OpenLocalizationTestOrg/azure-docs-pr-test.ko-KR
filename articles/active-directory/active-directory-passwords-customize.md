---
title: "사용자 지정: Azure AD SSPR | Microsoft Docs"
description: "Azure AD 셀프 서비스 암호 재설정에 대한 사용자 지정 옵션"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 8b9c120815473b25140b8717f8fdd539c97ebb04
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a><span data-ttu-id="8078b-103">셀프 서비스 암호 재설정을 위한 Azure AD 기능 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8078b-103">Customize Azure AD functionality for Self-Service Password Reset</span></span>

<span data-ttu-id="8078b-104">셀프 서비스 암호 재설정을 배포하려고 하는 IT 전문가는 사용자에게 맞게 환경을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-104">IT Professionals looking to deploy self-service password reset can customize the experience to match their users.</span></span>

## <a name="customize-the-contact-your-administrator-link"></a><span data-ttu-id="8078b-105">관리자에게 문의 링크 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8078b-105">Customize the contact your administrator link</span></span>

<span data-ttu-id="8078b-106">SSPR을 사용하지 않는 경우라도 사용자는 암호 재설정 포털에서 "관리자에게 문의" 링크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-106">Even if SSPR is not enabled users still a "contact your administrator" link on the password reset portal.</span></span>  <span data-ttu-id="8078b-107">이 링크를 클릭하면 사용자의 암호를 변경하는 데 도움을 요청하기 위해 관리자에게 전자 메일을 보내도록 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-107">Clicking this link emails your administrators asking for assistance in changing the user's password.</span></span> <span data-ttu-id="8078b-108">이 전자 메일은 다음 순서로 다음과 같은 받는 사람에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-108">This email is sent to the following recipients in the following order:</span></span>

1. <span data-ttu-id="8078b-109">**암호 관리자** 역할이 할당된 경우 이 역할을 가진 관리자에게 알림이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-109">If the **Password administrator** role is assigned, administrators with this role are notified</span></span>
2. <span data-ttu-id="8078b-110">암호 관리자가 할당되지 않은 경우 **사용자 관리자** 역할을 가진 관리자에게 알림이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-110">If no Password administrators are assigned, then administrators with the **User administrator** role are notified</span></span>
3. <span data-ttu-id="8078b-111">이전의 역할이 할당되지 않은 경우 **전역 관리자**가 표시됩니다</span><span class="sxs-lookup"><span data-stu-id="8078b-111">If neither of the previous roles were assigned, then **Global administrators** are notified</span></span>

<span data-ttu-id="8078b-112">어떠한 경우에도 최대 100명의 받는 사람에게 알림이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-112">In all cases, a maximum of 100 recipients are notified.</span></span>

<span data-ttu-id="8078b-113">다른 관리자 역할 및 할당하는 방법에 대해 자세히 알아보려면 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8078b-113">To find out more about the different administrator roles and how to assign them see the document [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span></span>

### <a name="disable-contact-your-administrator-emails"></a><span data-ttu-id="8078b-114">관리자에게 문의 전자 메일 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="8078b-114">Disable contact your administrator emails</span></span>

<span data-ttu-id="8078b-115">조직에서 관리자에게 암호 재설정 요청을 알리지 않으려는 경우 다음 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-115">If your organization does not want administrators notified about password reset requests, the following configuration can be enabled</span></span>

* <span data-ttu-id="8078b-116">모든 최종 사용자에게 셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="8078b-116">Enable self-service password reset for all end users.</span></span> <span data-ttu-id="8078b-117">이 옵션은 **암호 재설정 > 속성** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-117">This option is under **Password Reset > Properties**.</span></span>
    * <span data-ttu-id="8078b-118">사용자가 자신의 암호를 재설정할 수 없게 하려는 경우 빈 그룹에 대한 액세스 범위를 지정하면 됩니다. **이 옵션은 사용하지 않는 것이 좋습니다**.</span><span class="sxs-lookup"><span data-stu-id="8078b-118">If you do not wish users to reset their own passwords, you can scope access to an empty group **we do not recommend this option**.</span></span>
* <span data-ttu-id="8078b-119">사용자가 도움을 받을 수 있는 웹 URL 또는 mailto: 주소를 제공하는 고객 지원 센터 링크를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-119">Customize the helpdesk link to provide a web URL or mailto: address that users can use to get assistance.</span></span> <span data-ttu-id="8078b-120">이 옵션은 **암호 재설정 > 사용자 지정 > 사용자 지정 기술 지원 팀 메일 또는 URL** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-120">This option is under **Password Reset > Customization > Custom helpdesk email or URL**.</span></span>

## <a name="customize-adfs-sign-in-page-for-sspr"></a><span data-ttu-id="8078b-121">SSPR에 대한 ADFS 로그인 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8078b-121">Customize ADFS sign-in page for SSPR</span></span>

<span data-ttu-id="8078b-122">ADFS 관리자는 [Add sign-in page description](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description)(로그인 페이지 설정 추가) 문서의 지침에 따라 로그인 페이지 링크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-122">ADFS Administrators can add a link to their sign-in page using the guidance found in the article [Add sign-in page description](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).</span></span>

<span data-ttu-id="8078b-123">ADFS 서버에서 다음에 나오는 명령을 사용하면 사용자가 셀프 서비스 암호 재설정 워크플로를 직접 입력할 수 있는 ADFS 로그인 페이지의 링크가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-123">Using the command that follows on your ADFS server adds a link to the ADFS login page allowing users to enter the self-service password reset workflow directly.</span></span>

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-the-sign-in-and-access-panel-look-and-feel"></a><span data-ttu-id="8078b-124">로그인 및 액세스 패널 모양과 느낌 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8078b-124">Customize the sign-in and access panel look and feel</span></span>

<span data-ttu-id="8078b-125">사용자가 로그인 페이지에 액세스할 때 로그인 페이지 이미지와 함께 표시되는 로고를 회사 브랜딩에 맞게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-125">When your users access the login page, you can customize the logo that appears along with the sign-in page image to fit your company branding.</span></span>

<span data-ttu-id="8078b-126">다음과 같은 경우에는 이러한 그래픽이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-126">These graphics are shown in the following circumstances:</span></span>

* <span data-ttu-id="8078b-127">사용자가 사용자 이름을 입력한 후</span><span class="sxs-lookup"><span data-stu-id="8078b-127">After a user types their username</span></span>
* <span data-ttu-id="8078b-128">사용자가 사용자 지정된 URL에 액세스</span><span class="sxs-lookup"><span data-stu-id="8078b-128">User accesses customized url</span></span>
    * <span data-ttu-id="8078b-129">"Whr" 매개 변수를 "https://login.microsoftonline.com/?whr=contoso.com"과 같은 암호 재설정 페이지에 전달하는 방법</span><span class="sxs-lookup"><span data-stu-id="8078b-129">By passing the "whr" parameter to the password reset page, like "https://login.microsoftonline.com/?whr=contoso.com"</span></span>
    * <span data-ttu-id="8078b-130">"username" 매개 변수를 "https://login.microsoftonline.com/?username=admin@contoso.com"과 같은 암호 재설정 페이지에 전달하는 방법</span><span class="sxs-lookup"><span data-stu-id="8078b-130">By passing the "username" parameter to the password reset page, like "https://login.microsoftonline.com/?username=admin@contoso.com"</span></span>

### <a name="graphics-details"></a><span data-ttu-id="8078b-131">그래픽 정보</span><span class="sxs-lookup"><span data-stu-id="8078b-131">Graphics details</span></span>

<span data-ttu-id="8078b-132">다음 설정을 사용하면 로그인 페이지의 시각적 특성을 변경할 수 있습니다. 이 설정은 **Azure Active Directory**, **회사 브랜딩**, **회사 브랜딩 편집**에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-132">The following settings allow you to change the visual characteristics of the sign-in page and can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="8078b-133">로그인 페이지 이미지는 500KB 이하의 1420x1200픽셀인 JPG 또는 PNG 파일이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-133">Sign-in page image should be a PNG or JPG file 1420x1200 pixels and no larger than 500KB.</span></span> <span data-ttu-id="8078b-134">최상의 결과를 위해 약 200KB 정도가 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-134">We recommend it to be around 200 KB for best results.</span></span>
* <span data-ttu-id="8078b-135">로그인 페이지 배경색은 대기 시간이 긴 연결에서 작업하는 경우에 사용되고 RGB 16진수 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-135">Sign-in page background color is used when on high-latency connections and must be in the RGB hex format.</span></span>
* <span data-ttu-id="8078b-136">배너 이미지는 10KB 이하의 60x280픽셀인 JPG 또는 PNG 파일이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-136">Banner image should be a PNG or JPG file 60x280 pixels and no larger than 10 KB.</span></span>
* <span data-ttu-id="8078b-137">정사각형 로고(일반 및 어두운 테마)는 10KB 이하의 240x240(크기 조정 가능)픽셀인 JPG 또는 PNG 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-137">Square logo (normal and dark theme) PNG or JPG 240x240 (resizable) no larger than 10 KB.</span></span>

### <a name="sign-in-text-options"></a><span data-ttu-id="8078b-138">로그인 텍스트 옵션</span><span class="sxs-lookup"><span data-stu-id="8078b-138">Sign-in text options</span></span>

<span data-ttu-id="8078b-139">다음 설정을 사용하면 텍스트를 조직에 관련된 로그인 페이지에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-139">The following settings allow you to add text to the sign-in page relevant to your organization.</span></span> <span data-ttu-id="8078b-140">이러한 설정은 **Azure Active Directory**, **회사 브랜딩**, **회사 브랜딩 편집**에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-140">These settings can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="8078b-141">**사용자 이름 힌트**는 someone@example.com 텍스트의 예제를 사용자에게 보다 적합한 형태로 바꿉니다. 이 기능은 내부 및 외부 사용자를 지원할 때 기본으로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-141">**User name hint** replaces the example text of someone@example.com with something more appropriate for your users, recommended to be left default when supporting internal and external users</span></span>
* <span data-ttu-id="8078b-142">**로그인 페이지 텍스트**는 최대 256자입니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-142">**Sign-in page text** is a maximum of 256 characters in length.</span></span> <span data-ttu-id="8078b-143">이 텍스트는 사용자가 온라인으로 로그인하는 경우 및 Windows 10의 Azure AD 조인 경험에서 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-143">This text appears anywhere your users login online, and in the Azure AD Join experience on Windows 10.</span></span> <span data-ttu-id="8078b-144">사용 약관, 지침 및 사용자에 대한 팁에서 이 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-144">Use this text for terms of use, instructions, and tips for your users.</span></span> <span data-ttu-id="8078b-145">**누구든지 로그인 페이지를 볼 수 있으므로 여기에서 중요 정보를 제공하지 않도록 합니다.**</span><span class="sxs-lookup"><span data-stu-id="8078b-145">**Anyone can see your sign-in page so do not provide any sensitive information here.**</span></span>

### <a name="keep-me-signed-in-disabled"></a><span data-ttu-id="8078b-146">로그인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="8078b-146">Keep me signed in disabled</span></span>

<span data-ttu-id="8078b-147">“로그인 사용 안 함” 옵션을 사용하면 사용자가 해당 브라우저 창을 닫고 다시 열 때 로그인 상태를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-147">The option "Keep me signed in disabled" allows users to remain signed in when they close and reopen their browser window.</span></span> <span data-ttu-id="8078b-148">이 옵션은 세션 수명에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-148">This option does not impact session lifetimes.</span></span> <span data-ttu-id="8078b-149">이 설정은 **Azure Active Directory > 회사 브랜딩 > 회사 브랜딩 편집** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-149">This setting is found under **Azure Active Directory > Company branding > Edit company branding**.</span></span>

<span data-ttu-id="8078b-150">SharePoint Online과 Office 2010의 일부 기능은 이 확인란을 선택할 수 있는 사용자에 대한 종속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-150">Some features of SharePoint Online and Office 2010 have a dependency on users being able to check this box.</span></span> <span data-ttu-id="8078b-151">이 옵션을 숨기면 사용자에게 추가 및 예기치 않은 로그인 프롬프트가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-151">If you hide this option, users may get additional and unexpected sign-in prompts.</span></span>

### <a name="directory-name"></a><span data-ttu-id="8078b-152">디렉터리 이름</span><span class="sxs-lookup"><span data-stu-id="8078b-152">Directory name</span></span>

<span data-ttu-id="8078b-153">**Azure Active Directory > 속성** 아래에서 이름 특성을 변경하여 포털 및 자동화된 통신에서 친숙한 조직 이름을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-153">You can change the name attribute under **Azure Active Directory > Properties** to show a friendly organization name seen in the portal and automated communications.</span></span> <span data-ttu-id="8078b-154">이 옵션은 계속되는 양식에서 자동화된 전자 메일의 형태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-154">This option is most visible in the form of automated emails in the forms that follow</span></span>

* <span data-ttu-id="8078b-155">"CONTOSO 데모를 대신하는 Microsoft" 전자 메일의 친숙한 이름</span><span class="sxs-lookup"><span data-stu-id="8078b-155">Friendly name in email “Microsoft on behalf of CONTOSO demo”</span></span>
* <span data-ttu-id="8078b-156">"CONTOSO 데모 계정 전자 메일 확인 코드" 전자 메일의 제목 줄</span><span class="sxs-lookup"><span data-stu-id="8078b-156">Subject line in email “CONTOSO demo account email verification code”</span></span>

## <a name="next-steps"></a><span data-ttu-id="8078b-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8078b-157">Next steps</span></span>

<span data-ttu-id="8078b-158">다음 링크는 Azure AD를 사용한 암호 재설정에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-158">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="8078b-159">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="8078b-159">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="8078b-160">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="8078b-160">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="8078b-161">[**데이터**](active-directory-passwords-data.md) - 암호 관리에 필요한 데이터 및 사용 방식을 이해</span><span class="sxs-lookup"><span data-stu-id="8078b-161">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="8078b-162">[**롤아웃**](active-directory-passwords-best-practices.md) - 여기서 제공하는 지침을 사용하여 배포 계획을 세우고 사용자에게 SSPR 배포</span><span class="sxs-lookup"><span data-stu-id="8078b-162">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="8078b-163">[**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정</span><span class="sxs-lookup"><span data-stu-id="8078b-163">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="8078b-164">[**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리</span><span class="sxs-lookup"><span data-stu-id="8078b-164">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="8078b-165">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="8078b-165">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="8078b-166">[**기술 심층 분석**](active-directory-passwords-how-it-works.md) - 작동 방식을 이해하기 위해 심층 분석</span><span class="sxs-lookup"><span data-stu-id="8078b-166">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="8078b-167">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="8078b-167">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="8078b-168">그 이유는</span><span class="sxs-lookup"><span data-stu-id="8078b-168">Why?</span></span> <span data-ttu-id="8078b-169">무엇을?</span><span class="sxs-lookup"><span data-stu-id="8078b-169">What?</span></span> <span data-ttu-id="8078b-170">어디서?</span><span class="sxs-lookup"><span data-stu-id="8078b-170">Where?</span></span> <span data-ttu-id="8078b-171">누가?</span><span class="sxs-lookup"><span data-stu-id="8078b-171">Who?</span></span> <span data-ttu-id="8078b-172">언제?</span><span class="sxs-lookup"><span data-stu-id="8078b-172">When?</span></span> <span data-ttu-id="8078b-173">- 많은 분들이 항상 묻는 질문에 대한 답변입니다.</span><span class="sxs-lookup"><span data-stu-id="8078b-173">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="8078b-174">[**문제 해결**](active-directory-passwords-troubleshoot.md) - SSPR의 일반적인 문제 해결 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="8078b-174">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>


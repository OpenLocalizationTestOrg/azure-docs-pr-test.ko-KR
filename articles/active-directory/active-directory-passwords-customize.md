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
ms.openlocfilehash: 4762fffef040f9b409355f9ee0e8cc593e3eea0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a><span data-ttu-id="5441d-103">셀프 서비스 암호 재설정을 위한 Azure AD 기능 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="5441d-103">Customize Azure AD functionality for Self-Service Password Reset</span></span>

<span data-ttu-id="5441d-104">IT 전문가 toodeploy 셀프 서비스 암호 재설정을 찾고 사용자 지정할 수 hello 경험 toomatch 사용자.</span><span class="sxs-lookup"><span data-stu-id="5441d-104">IT Professionals looking toodeploy self-service password reset can customize hello experience toomatch their users.</span></span>

## <a name="customize-hello-contact-your-administrator-link"></a><span data-ttu-id="5441d-105">Hello 연락처 관리자 링크를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="5441d-105">Customize hello contact your administrator link</span></span>

<span data-ttu-id="5441d-106">경우에 SSPR 사용 되는 사용자 여전히는 "관리자에 게 문의" 링크 hello 암호 재설정 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-106">Even if SSPR is not enabled users still a "contact your administrator" link on hello password reset portal.</span></span>  <span data-ttu-id="5441d-107">이 링크를 클릭 하면 hello 사용자의 암호 변경에 대 한 도움말을 요청 하는 관리자에 게 문의 전자 메일로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-107">Clicking this link emails your administrators asking for assistance in changing hello user's password.</span></span> <span data-ttu-id="5441d-108">이 전자 메일은 다음 순서에 따라 hello에서 받는 사람 toohello를 전송 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-108">This email is sent toohello following recipients in hello following order:</span></span>

1. <span data-ttu-id="5441d-109">경우 hello **암호 관리자** 역할이 할당 될,이 역할이 있는 관리자는 알림을</span><span class="sxs-lookup"><span data-stu-id="5441d-109">If hello **Password administrator** role is assigned, administrators with this role are notified</span></span>
2. <span data-ttu-id="5441d-110">하는 경우 암호 관리자 할당 되었는지, 다음 hello로 관리자 **사용자 관리자** 역할 알림이 표시 됩니다</span><span class="sxs-lookup"><span data-stu-id="5441d-110">If no Password administrators are assigned, then administrators with hello **User administrator** role are notified</span></span>
3. <span data-ttu-id="5441d-111">경우 모두 hello 앞의 역할 할당, 다음 **전역 관리자** 알림이 표시 됩니다</span><span class="sxs-lookup"><span data-stu-id="5441d-111">If neither of hello previous roles were assigned, then **Global administrators** are notified</span></span>

<span data-ttu-id="5441d-112">어떠한 경우에도 최대 100명의 받는 사람에게 알림이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-112">In all cases, a maximum of 100 recipients are notified.</span></span>

<span data-ttu-id="5441d-113">hello 다른 관리자 역할 및 tooassign 해당 참조 문서 hello 하는 방법에 대 한 자세한 내용을 toofind [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="5441d-113">toofind out more about hello different administrator roles and how tooassign them see hello document [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span></span>

### <a name="disable-contact-your-administrator-emails"></a><span data-ttu-id="5441d-114">관리자에게 문의 전자 메일 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="5441d-114">Disable contact your administrator emails</span></span>

<span data-ttu-id="5441d-115">조직에서 관리자 암호에 대 한 알림을 다시 설정 요청을 원치 않을 경우 hello 다음 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-115">If your organization does not want administrators notified about password reset requests, hello following configuration can be enabled</span></span>

* <span data-ttu-id="5441d-116">모든 최종 사용자에게 셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="5441d-116">Enable self-service password reset for all end users.</span></span> <span data-ttu-id="5441d-117">이 옵션은 **암호 재설정 > 속성** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-117">This option is under **Password Reset > Properties**.</span></span>
    * <span data-ttu-id="5441d-118">싶지 않은 사용자가 tooreset 자신의 암호를 하는 경우 범위를 지정 하면 액세스 tooan 빈 그룹 **이 옵션은 좋지 않습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-118">If you do not wish users tooreset their own passwords, you can scope access tooan empty group **we do not recommend this option**.</span></span>
* <span data-ttu-id="5441d-119">웹 URL 또는 mailto hello 기술 지원팀 링크 tooprovide 사용자 지정: 사용자가 tooget 지원을 사용할 수 있는 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-119">Customize hello helpdesk link tooprovide a web URL or mailto: address that users can use tooget assistance.</span></span> <span data-ttu-id="5441d-120">이 옵션은 **암호 재설정 > 사용자 지정 > 사용자 지정 기술 지원 팀 메일 또는 URL** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-120">This option is under **Password Reset > Customization > Custom helpdesk email or URL**.</span></span>

## <a name="customize-adfs-sign-in-page-for-sspr"></a><span data-ttu-id="5441d-121">SSPR에 대한 ADFS 로그인 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="5441d-121">Customize ADFS sign-in page for SSPR</span></span>

<span data-ttu-id="5441d-122">Ad FS 관리자는 링크 tootheir 로그인 페이지의 hello 문서 hello 지침을 사용 하 여 추가할 수 있습니다 [로그인 페이지 설명을 추가](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description)합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-122">ADFS Administrators can add a link tootheir sign-in page using hello guidance found in hello article [Add sign-in page description](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).</span></span>

<span data-ttu-id="5441d-123">ADFS 서버에서 다음에 나오는 hello 명령을 사용 하 여 사용자가 tooenter hello 셀프 서비스 암호 재설정 워크플로 직접 허용 링크 toohello ADFS 로그인 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-123">Using hello command that follows on your ADFS server adds a link toohello ADFS login page allowing users tooenter hello self-service password reset workflow directly.</span></span>

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a><span data-ttu-id="5441d-124">Hello 로그인 및 액세스 패널 모양 및 느낌을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="5441d-124">Customize hello sign-in and access panel look and feel</span></span>

<span data-ttu-id="5441d-125">Hello 로그인 페이지에 액세스 하는 사용자가 회사 브랜딩을 hello 로그인 페이지 이미지 toofit 함께 나타나는 hello 로고를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-125">When your users access hello login page, you can customize hello logo that appears along with hello sign-in page image toofit your company branding.</span></span>

<span data-ttu-id="5441d-126">이러한 그래픽 hello 상황 뒤에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-126">These graphics are shown in hello following circumstances:</span></span>

* <span data-ttu-id="5441d-127">사용자가 사용자 이름을 입력한 후</span><span class="sxs-lookup"><span data-stu-id="5441d-127">After a user types their username</span></span>
* <span data-ttu-id="5441d-128">사용자가 사용자 지정된 URL에 액세스</span><span class="sxs-lookup"><span data-stu-id="5441d-128">User accesses customized url</span></span>
    * <span data-ttu-id="5441d-129">Hello 전달 하 여 "whr" 매개 변수 toohello 암호 재설정 페이지 "https://login.microsoftonline.com/?whr=contoso.com"와 같은</span><span class="sxs-lookup"><span data-stu-id="5441d-129">By passing hello "whr" parameter toohello password reset page, like "https://login.microsoftonline.com/?whr=contoso.com"</span></span>
    * <span data-ttu-id="5441d-130">Hello "username"을 전달 하 여 매개 변수 toohello 암호 재설정 페이지에 같은 "https://login.microsoftonline.com/?username=admin@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="5441d-130">By passing hello "username" parameter toohello password reset page, like "https://login.microsoftonline.com/?username=admin@contoso.com"</span></span>

### <a name="graphics-details"></a><span data-ttu-id="5441d-131">그래픽 정보</span><span class="sxs-lookup"><span data-stu-id="5441d-131">Graphics details</span></span>

<span data-ttu-id="5441d-132">hello 다음 toochange hello hello 로그인 페이지의 시각적 특성을 사용 하면 설정과 확인할 수 있습니다 **Azure Active Directory**, **회사 브랜딩**, **회사 편집 브랜딩**</span><span class="sxs-lookup"><span data-stu-id="5441d-132">hello following settings allow you toochange hello visual characteristics of hello sign-in page and can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="5441d-133">로그인 페이지 이미지는 500KB 이하의 1420x1200픽셀인 JPG 또는 PNG 파일이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-133">Sign-in page image should be a PNG or JPG file 1420x1200 pixels and no larger than 500KB.</span></span> <span data-ttu-id="5441d-134">Toobe 약 200KB 최상의 결과 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-134">We recommend it toobe around 200 KB for best results.</span></span>
* <span data-ttu-id="5441d-135">로그인 페이지 배경색 대기 시간이 긴 연결에서 사용 되 고 hello RGB 16 진수 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-135">Sign-in page background color is used when on high-latency connections and must be in hello RGB hex format.</span></span>
* <span data-ttu-id="5441d-136">배너 이미지는 10KB 이하의 60x280픽셀인 JPG 또는 PNG 파일이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-136">Banner image should be a PNG or JPG file 60x280 pixels and no larger than 10 KB.</span></span>
* <span data-ttu-id="5441d-137">정사각형 로고(일반 및 어두운 테마)는 10KB 이하의 240x240(크기 조정 가능)픽셀인 JPG 또는 PNG 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-137">Square logo (normal and dark theme) PNG or JPG 240x240 (resizable) no larger than 10 KB.</span></span>

### <a name="sign-in-text-options"></a><span data-ttu-id="5441d-138">로그인 텍스트 옵션</span><span class="sxs-lookup"><span data-stu-id="5441d-138">Sign-in text options</span></span>

<span data-ttu-id="5441d-139">다음 설정을 hello를 사용 하면 tooadd 텍스트 toohello 로그인 페이지 관련 tooyour 조직 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-139">hello following settings allow you tooadd text toohello sign-in page relevant tooyour organization.</span></span> <span data-ttu-id="5441d-140">이러한 설정은 **Azure Active Directory**, **회사 브랜딩**, **회사 브랜딩 편집**에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-140">These settings can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="5441d-141">**사용자 이름 힌트** 대체 hello의 예제 텍스트 someone@example.com 내부 및 외부 사용자를 지 원하는 경우 사용자에 게 보다 적합 한 형태로와 toobe 왼쪽된 기본에 권장</span><span class="sxs-lookup"><span data-stu-id="5441d-141">**User name hint** replaces hello example text of someone@example.com with something more appropriate for your users, recommended toobe left default when supporting internal and external users</span></span>
* <span data-ttu-id="5441d-142">**로그인 페이지 텍스트**는 최대 256자입니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-142">**Sign-in page text** is a maximum of 256 characters in length.</span></span> <span data-ttu-id="5441d-143">이 텍스트 온라인 및 hello Windows 10에서 Azure AD 조인 환경에 사용자가 로그인 아무 곳 이나 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-143">This text appears anywhere your users login online, and in hello Azure AD Join experience on Windows 10.</span></span> <span data-ttu-id="5441d-144">사용 약관, 지침 및 사용자에 대한 팁에서 이 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-144">Use this text for terms of use, instructions, and tips for your users.</span></span> <span data-ttu-id="5441d-145">**누구든지 로그인 페이지를 볼 수 있으므로 여기에서 중요 정보를 제공하지 않도록 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5441d-145">**Anyone can see your sign-in page so do not provide any sensitive information here.**</span></span>

### <a name="keep-me-signed-in-disabled"></a><span data-ttu-id="5441d-146">로그인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="5441d-146">Keep me signed in disabled</span></span>

<span data-ttu-id="5441d-147">hello 옵션 "로그인 유지 사용 안 함" 브라우저 창을 닫았다가 때 로그인 하는 사용자가 tooremain을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-147">hello option "Keep me signed in disabled" allows users tooremain signed in when they close and reopen their browser window.</span></span> <span data-ttu-id="5441d-148">이 옵션은 세션 수명에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-148">This option does not impact session lifetimes.</span></span> <span data-ttu-id="5441d-149">이 설정은 **Azure Active Directory > 회사 브랜딩 > 회사 브랜딩 편집** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-149">This setting is found under **Azure Active Directory > Company branding > Edit company branding**.</span></span>

<span data-ttu-id="5441d-150">SharePoint Online 및 Office 2010의 일부 기능 사용자가 수 toocheck이이 상자에는 종속성이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-150">Some features of SharePoint Online and Office 2010 have a dependency on users being able toocheck this box.</span></span> <span data-ttu-id="5441d-151">이 옵션을 숨기면 사용자에게 추가 및 예기치 않은 로그인 프롬프트가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-151">If you hide this option, users may get additional and unexpected sign-in prompts.</span></span>

### <a name="directory-name"></a><span data-ttu-id="5441d-152">디렉터리 이름</span><span class="sxs-lookup"><span data-stu-id="5441d-152">Directory name</span></span>

<span data-ttu-id="5441d-153">아래에 hello 이름 특성을 변경할 수 있습니다 **Azure Active Directory > 속성** tooshow 친숙 한 조직 이름 hello 포털에서 확인 했 고 자동으로 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-153">You can change hello name attribute under **Azure Active Directory > Properties** tooshow a friendly organization name seen in hello portal and automated communications.</span></span> <span data-ttu-id="5441d-154">이 옵션은 다음에 나오는 hello 형태로 자동화 된 전자 메일의 hello 형태로 가장 눈에 띄는</span><span class="sxs-lookup"><span data-stu-id="5441d-154">This option is most visible in hello form of automated emails in hello forms that follow</span></span>

* <span data-ttu-id="5441d-155">"CONTOSO 데모를 대신하는 Microsoft" 전자 메일의 친숙한 이름</span><span class="sxs-lookup"><span data-stu-id="5441d-155">Friendly name in email “Microsoft on behalf of CONTOSO demo”</span></span>
* <span data-ttu-id="5441d-156">"CONTOSO 데모 계정 전자 메일 확인 코드" 전자 메일의 제목 줄</span><span class="sxs-lookup"><span data-stu-id="5441d-156">Subject line in email “CONTOSO demo account email verification code”</span></span>

## <a name="next-steps"></a><span data-ttu-id="5441d-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5441d-157">Next steps</span></span>

<span data-ttu-id="5441d-158">링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5441d-158">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="5441d-159">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="5441d-159">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="5441d-160">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="5441d-160">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="5441d-161">[**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법</span><span class="sxs-lookup"><span data-stu-id="5441d-161">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="5441d-162">[**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자</span><span class="sxs-lookup"><span data-stu-id="5441d-162">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="5441d-163">[**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정</span><span class="sxs-lookup"><span data-stu-id="5441d-163">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="5441d-164">[**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리</span><span class="sxs-lookup"><span data-stu-id="5441d-164">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="5441d-165">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="5441d-165">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="5441d-166">[**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법</span><span class="sxs-lookup"><span data-stu-id="5441d-166">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="5441d-167">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="5441d-167">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="5441d-168">그 이유는</span><span class="sxs-lookup"><span data-stu-id="5441d-168">Why?</span></span> <span data-ttu-id="5441d-169">무엇을?</span><span class="sxs-lookup"><span data-stu-id="5441d-169">What?</span></span> <span data-ttu-id="5441d-170">어디서?</span><span class="sxs-lookup"><span data-stu-id="5441d-170">Where?</span></span> <span data-ttu-id="5441d-171">누가?</span><span class="sxs-lookup"><span data-stu-id="5441d-171">Who?</span></span> <span data-ttu-id="5441d-172">언제?</span><span class="sxs-lookup"><span data-stu-id="5441d-172">When?</span></span> <span data-ttu-id="5441d-173">-Tooask 항상 필요한 tooquestions 답변</span><span class="sxs-lookup"><span data-stu-id="5441d-173">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="5441d-174">[**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="5441d-174">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>


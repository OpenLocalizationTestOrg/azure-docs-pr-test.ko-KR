---
title: "Azure Active directory에서 B2B 공동 작업에 대 한 aaaConfigure SaaS 앱 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업을 위한 코드 및 PowerShell 샘플"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="e14fc-103">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="e14fc-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="e14fc-104">Azure AD(Azure Active Directory) B2B 공동 작업은 Azure AD와 통합되는 대부분의 앱에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="e14fc-105">이 섹션에서는 Azure AD B2B와 함께 사용되는 일부 인기 있는 SaaS 앱을 구성하는 지침을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="e14fc-106">앱별 지침을 살펴보기 전에 다음과 같이 경험에 근거한 몇 가지 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="e14fc-107">Hello 앱의 대부분의 경우 사용자 설정을 수동으로 toohappen이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-107">For most of hello apps, user setup needs toohappen manually.</span></span> <span data-ttu-id="e14fc-108">즉, 사용자가 직접 만들어야 합니다 hello 응용 프로그램의 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-108">That is, users must be created manually in hello app as well.</span></span>

* <span data-ttu-id="e14fc-109">Dropbox, 예: 자동 설치를 지원 되는 앱에 대 한 별도 초대 hello 앱에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from hello apps.</span></span> <span data-ttu-id="e14fc-110">사용자가 각 초대 있는지 tooaccept 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-110">Users must be sure tooaccept each invitation.</span></span>

* <span data-ttu-id="e14fc-111">게스트 사용자의 변환 된 사용자 프로필 디스크 (UPD)와 문제가 toomitigate hello 사용자 특성에 항상 설정 **사용자 식별자** 너무**user.mail**합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-111">In hello user attributes, toomitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** too**user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="e14fc-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="e14fc-112">Dropbox Business</span></span>

<span data-ttu-id="e14fc-113">자신의 조직 계정을 사용 하 여 tooenable 사용자 toosign, SAML Security Assertion Markup Language () id 공급자로 Dropbox 비즈니스 toouse Azure AD를 수동으로 구성 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-113">tooenable users toosign in using their organization account, you must manually configure Dropbox Business toouse Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="e14fc-114">Dropbox 비즈니스 toodo 구성된 되지 않은 경우, 메시지를 표시 하거나 없습니다 허용 하는 Azure AD를 사용 하 여 사용자가 toosign 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-114">If Dropbox Business has not been configured toodo so, it cannot prompt or otherwise allow users toosign in using Azure AD.</span></span>

1. <span data-ttu-id="e14fc-115">선택 하는 Azure AD에 tooadd hello Dropbox 비즈니스 앱 **엔터프라이즈 응용 프로그램** 왼쪽된 창의 hello와 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-115">tooadd hello Dropbox Business app into Azure AD, select **Enterprise applications** in hello left pane, and then click **Add**.</span></span>

  ![hello 엔터프라이즈 응용 프로그램 페이지에서 hello "추가" 단추](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="e14fc-117">Hello에 **응용 프로그램 추가** 창 입력 **dropbox** 에 hello 검색 상자를 클릭 한 **Dropbox for Business** hello 결과 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-117">In hello **Add an application** window, enter **dropbox** in hello search box, and then select **Dropbox for Business** in hello results list.</span></span>

  !["Dropbox" hello에 대 한 검색 응용 프로그램 페이지 추가](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="e14fc-119">Hello에 **Single sign on** 페이지에서 **Single sign on** 에 hello 왼쪽된 창에서 선택한 다음 입력 **user.mail** hello에 **사용자 식별자** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-119">On hello **Single sign-on** page, select **Single sign-on** in hello left pane, and then enter **user.mail** in hello **User Identifier** box.</span></span> <span data-ttu-id="e14fc-120">(기본적으로 UPN으로 설정됩니다.)</span><span class="sxs-lookup"><span data-stu-id="e14fc-120">(It's set as UPN by default.)</span></span>

  ![Single sign on hello 앱에 대 한 구성](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="e14fc-122">toodownload hello 인증서 toouse Dropbox 구성에 대 한 선택 **DropBox 구성**를 선택한 후 **SAML Single Sign-on 서비스 URL** hello 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-122">toodownload hello certificate toouse for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in hello list.</span></span>

  ![Dropbox 구성에 대 한 hello 인증서를 다운로드합니다.](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="e14fc-124">Hello로 tooDropbox 로그인 로그온 URL에서 hello **Single sign on** 페이지.</span><span class="sxs-lookup"><span data-stu-id="e14fc-124">Sign in tooDropbox with hello sign-on URL from hello **Single sign-on** page.</span></span>

  ![Dropbox 로그인 hello 페이지](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="e14fc-126">Hello 메뉴에서 선택 **관리 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-126">On hello menu, select **Admin Console**.</span></span>

  ![hello Dropbox 메뉴의 hello "관리 콘솔" 링크](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="e14fc-128">Hello에 **인증** 대화 상자에서 **자세한**, hello 인증서를 업로드 한 다음 hello **로그인 URL** 상자 hello SAML single sign on URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-128">In hello **Authentication** dialog box, select **More**, upload hello certificate and then, in hello **Sign in URL** box, enter hello SAML single sign-on URL.</span></span>

  ![hello 축소 hello 인증 대화 상자에서 "추가" 링크](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![hello에 "로그인 URL" hello 확장 인증 대화 상자](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="e14fc-131">hello Azure 포털에서에서 설치 프로그램을 tooconfigure 자동 사용자 선택 **프로 비전** hello 왼쪽된 창에서 선택 **자동** hello에 **프로 비전 모드** 상자를 선택한 후 **권한을 부여**합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-131">tooconfigure automatic user setup in hello Azure portal, select **Provisioning** in hello left pane, select **Automatic** in hello **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Hello Azure 포털에에서 자동 사용자 프로비저닝 구성](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="e14fc-133">멤버 또는 게스트 사용자에 게는 hello Dropbox 응용 프로그램에서 설정 되는 Dropbox에서 별도 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-133">After guest or member users have been set up in hello Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="e14fc-134">Dropbox에 single sign-on toouse, 초대 된 사람이 해당 링크를 클릭 하 여 hello 초대를 동의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-134">toouse Dropbox single sign-on, invitees must accept hello invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="e14fc-135">Box</span><span class="sxs-lookup"><span data-stu-id="e14fc-135">Box</span></span>
<span data-ttu-id="e14fc-136">Hello SAML 프로토콜을 기반으로 하는 페더레이션을 사용 하 여 사용자가 tooauthenticate 상자 게스트 사용자가 Azure AD 계정으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-136">You can enable users tooauthenticate Box guest users with their Azure AD account by using federation that's based on hello SAML protocol.</span></span> <span data-ttu-id="e14fc-137">이 절차에서는 tooBox.com 메타 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-137">In this procedure, you upload metadata tooBox.com.</span></span>

1. <span data-ttu-id="e14fc-138">Hello 엔터프라이즈 응용 프로그램에서 hello 상자 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-138">Add hello Box app from hello enterprise apps.</span></span>

2. <span data-ttu-id="e14fc-139">순서에 따라 hello에서 single sign on 구성:</span><span class="sxs-lookup"><span data-stu-id="e14fc-139">Configure single sign-on in hello following order:</span></span>

  ![Box Single Sign-On 구성](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="e14fc-141">a.</span><span class="sxs-lookup"><span data-stu-id="e14fc-141">a.</span></span> <span data-ttu-id="e14fc-142">Hello에 **로그온 URL** hello 로그온 URL에에서 설정 되어 있는지 적절 하 게 상자에 대 한 hello Azure 포털을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-142">In hello **Sign on URL** box, ensure that hello sign-on URL is set appropriately for Box in hello Azure portal.</span></span> <span data-ttu-id="e14fc-143">이 URL은 Box.com 테 넌 트의 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-143">This URL is hello URL of your Box.com tenant.</span></span> <span data-ttu-id="e14fc-144">Hello 명명 규칙을 따라야 *https://.box.com*합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-144">It should follow hello naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="e14fc-145">hello **식별자** toothis 적용 되지 않습니다 하지만 응용 프로그램을 여전히 필드는 필수로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-145">hello **Identifier** does not apply toothis app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="e14fc-146">b.</span><span class="sxs-lookup"><span data-stu-id="e14fc-146">b.</span></span> <span data-ttu-id="e14fc-147">Hello에 **사용자 식별자** 상자에 입력 **user.mail** (게스트 계정에 대 한 SSO)에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-147">In hello **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="e14fc-148">c.</span><span class="sxs-lookup"><span data-stu-id="e14fc-148">c.</span></span> <span data-ttu-id="e14fc-149">**SAML 서명 인증서**에서 **새 인증서 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="e14fc-150">d.</span><span class="sxs-lookup"><span data-stu-id="e14fc-150">d.</span></span> <span data-ttu-id="e14fc-151">Box.com 테 넌 트 toouse Azure AD를 id 공급자로 구성 toobegin hello 메타 데이터 파일을 다운로드 하 고 tooyour 로컬 드라이브 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-151">toobegin configuring your Box.com tenant toouse Azure AD as an identity provider, download hello metadata file and then save it tooyour local drive.</span></span>

 <span data-ttu-id="e14fc-152">e.</span><span class="sxs-lookup"><span data-stu-id="e14fc-152">e.</span></span> <span data-ttu-id="e14fc-153">Hello 메타 데이터 파일 toohello 상자 지원 팀에 속하는 single sign on을 구성을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-153">Forward hello metadata file toohello Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="e14fc-154">Hello 왼쪽된 창에서 Azure AD 자동 사용자 설치에 대 한 선택 **프로 비전**를 선택한 후 **Authorize**합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-154">For Azure AD automatic user setup, in hello left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Azure AD tooconnect tooBox 권한 부여](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="e14fc-156">Dropbox 초대와 같은 상자 초대 된 사람이 hello 상자 응용 프로그램에서 자신의 초대를 교환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e14fc-156">Like Dropbox invitees, Box invitees must redeem their invitation from hello Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e14fc-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e14fc-157">Next steps</span></span>

<span data-ttu-id="e14fc-158">Hello 다음 Azure AD B2B 공동 작업에 대 한 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e14fc-158">See hello following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="e14fc-159">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="e14fc-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="e14fc-160">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="e14fc-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="e14fc-161">B2B 공동 작업 사용자 tooa 역할 추가</span><span class="sxs-lookup"><span data-stu-id="e14fc-161">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="e14fc-162">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="e14fc-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="e14fc-163">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="e14fc-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="e14fc-164">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="e14fc-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="e14fc-165">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="e14fc-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="e14fc-166">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="e14fc-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="e14fc-167">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="e14fc-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="e14fc-168">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="e14fc-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)

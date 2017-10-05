---
title: "Azure Active Directory에서 B2B 공동 작업을 위한 SaaS 앱 구성 | Microsoft Docs"
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
ms.openlocfilehash: 149a493f7b369415f0a2726dd6a576f0195c13d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="15e76-103">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="15e76-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="15e76-104">Azure AD(Azure Active Directory) B2B 공동 작업은 Azure AD와 통합되는 대부분의 앱에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="15e76-105">이 섹션에서는 Azure AD B2B와 함께 사용되는 일부 인기 있는 SaaS 앱을 구성하는 지침을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="15e76-106">앱별 지침을 살펴보기 전에 다음과 같이 경험에 근거한 몇 가지 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="15e76-107">대부분의 앱에서 사용자 설치는 수동으로 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="15e76-108">즉, 앱에서도 사용자를 수동으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="15e76-109">Dropbox처럼 자동 설치를 지원하는 앱의 경우 앱에서 별도의 초대가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="15e76-110">사용자는 각 초대를 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="15e76-111">게스트 사용자의 잘못된(mangled) UPD(사용자 프로필 디스크) 관련 문제를 완화할 수 있도록 사용자 특성에서 항상 **사용자 식별자**를 **user.mail**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="15e76-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="15e76-112">Dropbox Business</span></span>

<span data-ttu-id="15e76-113">사용자가 조직 계정을 사용하여 로그인할 수 있게 하려면 SAML(Security Assertion Markup Language) ID 공급자로 Azure AD를 사용하도록 수동으로 Dropbox Business를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="15e76-114">Dropbox Business가 그렇게 구성되지 않으면 프롬프트를 표시할 수 없거나 사용자가 Azure AD를 사용하여 로그인할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="15e76-115">Azure AD에 Dropbox Business를 추가하려면 왼쪽 창에서 **엔터프라이즈 응용 프로그램**을 선택한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![엔터프라이즈 응용 프로그램 페이지의 "추가" 단추](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="15e76-117">**응용 프로그램 추가** 창의 검색 상자에 **dropbox**를 입력한 다음 결과 목록에서 **Dropbox for Business**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![응용 프로그램 추가 페이지에서 "dropbox" 검색](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="15e76-119">**Single Sign-On** 페이지의 왼쪽 창에서 **Single Sign-On**을 선택한 다음 **사용자 식별자** 상자에 **user.mail**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="15e76-120">(기본적으로 UPN으로 설정됩니다.)</span><span class="sxs-lookup"><span data-stu-id="15e76-120">(It's set as UPN by default.)</span></span>

  ![앱에 Single Sign-On 구성](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="15e76-122">Dropbox 구성에 사용할 인증서를 다운로드하려면 **DropBox 구성**을 선택한 다음 목록에서 **SAML Single Sign-On 서비스 URL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![Dropbox 구성에 사용할 인증서 다운로드](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="15e76-124">**Single Sign-On** 페이지에서 로그온 URL을 사용하여 Dropbox에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![Dropbox 로그인 페이지](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="15e76-126">메뉴에서 **관리 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-126">On the menu, select **Admin Console**.</span></span>

  ![Dropbox 메뉴의 "관리 콘솔" 링크](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="15e76-128">**인증** 대화 상자에서 **추가**를 선택하고, 인증서를 업로드한 다음 **로그인 URL** 상자에 SAML Single Sign-On URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![축소된 인증 대화 상자의 "추가" 링크](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![확장된 인증 대화 상자의 "로그인 URL"](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="15e76-131">Azure Portal에서 자동 사용자 설치를 구성하려면 왼쪽 창에서 **프로비전**을 선택하고, **프로비전 모드** 상자에서 **자동**을 선택한 다음 **권한 부여**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Azure Portal에서 자동 사용자 프로비전 구성](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="15e76-133">Dropbox 앱에서 게스트 또는 멤버 사용자가 설정되면 사용자가 Dropbox에서 별도의 초대를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="15e76-134">Dropbox Single Sign-On을 사용하려면 초대 받는 사람이 초대 안에 포함된 링크를 클릭하여 초대를 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="15e76-135">Box</span><span class="sxs-lookup"><span data-stu-id="15e76-135">Box</span></span>
<span data-ttu-id="15e76-136">SAML 프로토콜 기반의 페더레이션을 사용하여 사용자의 Azure AD 계정으로 Box 게스트 사용자를 인증하도록 사용자를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="15e76-137">이 절차에서 Box.com에 메타데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="15e76-138">엔터프라이즈 앱에서 Box 앱을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="15e76-139">다음 순서로 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-139">Configure single sign-on in the following order:</span></span>

  ![Box Single Sign-On 구성](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="15e76-141">a.</span><span class="sxs-lookup"><span data-stu-id="15e76-141">a.</span></span> <span data-ttu-id="15e76-142">**로그온 URL** 상자에서 Azure Portal의 Box에 대해 로그온 URL이 적합하게 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="15e76-143">이 URL은 Box.com 테넌트의 URL이며</span><span class="sxs-lookup"><span data-stu-id="15e76-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="15e76-144">*https://.box.com* 명명 규칙을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="15e76-145">**식별자**는 이 앱에 적용되지 않지만 여전히 필수 필드로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="15e76-146">b.</span><span class="sxs-lookup"><span data-stu-id="15e76-146">b.</span></span> <span data-ttu-id="15e76-147">**사용자 식별자** 상자에 **user.mail**(게스트 계정의 SSO에 대한)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="15e76-148">c.</span><span class="sxs-lookup"><span data-stu-id="15e76-148">c.</span></span> <span data-ttu-id="15e76-149">**SAML 서명 인증서**에서 **새 인증서 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="15e76-150">d.</span><span class="sxs-lookup"><span data-stu-id="15e76-150">d.</span></span> <span data-ttu-id="15e76-151">ID 공급자로 Azure AD를 사용하도록 Box.com 테넌트를 구성하려면 메타데이터 파일을 다운로드하여 로컬 드라이브에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="15e76-152">e.</span><span class="sxs-lookup"><span data-stu-id="15e76-152">e.</span></span> <span data-ttu-id="15e76-153">메타데이터 파일을 Box 지원 팀에 전달합니다. 그러면 지원 팀에서 대신 Single Sign-On을 구성할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="15e76-154">Azure AD 자동 사용자 설치의 경우 왼쪽 창에서 **프로비전**을 선택한 다음 **권한 부여**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Box에 연결하도록 Azure AD에 권한 부여](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="15e76-156">Dropbox 초대 대상자와 마찬가지로 Box 초대 대상자는 Box 앱의 초대를 교환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15e76-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15e76-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="15e76-157">Next steps</span></span>

<span data-ttu-id="15e76-158">Azure AD B2B 공동 작업에 대한 다음 문서를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="15e76-158">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="15e76-159">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="15e76-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="15e76-160">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="15e76-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="15e76-161">역할에 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="15e76-161">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="15e76-162">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="15e76-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="15e76-163">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="15e76-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="15e76-164">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="15e76-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="15e76-165">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="15e76-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="15e76-166">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="15e76-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="15e76-167">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="15e76-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="15e76-168">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="15e76-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)

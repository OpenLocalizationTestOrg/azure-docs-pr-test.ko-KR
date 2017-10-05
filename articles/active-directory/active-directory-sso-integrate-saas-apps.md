---
title: "Azure Active Directory Single Sign-On과 SaaS 앱 통합 | Microsoft Docs"
description: "Azure Active Directory에서 SaaS 앱의 Single Sign-On 인증과 사용자 프로비전 집중식 액세스 관리를 사용하도록 설정합니다. SaaS 앱에 Azure Active Directory를 통합하는 방법의 개요입니다."
services: active-directory
keywords: "Azure AD와 SaaS 앱 통합"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fc0d297598c334ca8f6f8a2bd3ae948c87956342
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a><span data-ttu-id="0f649-105">Azure Active Directory Single Sign-On과 SaaS 앱 통합</span><span class="sxs-lookup"><span data-stu-id="0f649-105">Integrate Azure Active Directory single sign-on with SaaS apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f649-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0f649-106">Azure portal</span></span>](active-directory-enterprise-apps-manage-sso.md)
> * [<span data-ttu-id="0f649-107">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="0f649-107">Azure classic portal</span></span>](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

<span data-ttu-id="0f649-108">조직으로 가져오는 앱에 대한 Single Sign-On 설정을 시작하려면 Azure AD(Azure Active Directory)에서 기존 디렉터리를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-108">To get started setting up single sign-on for an app that you’re bringing into your organization, you will be using an existing directory in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0f649-109">Microsoft Azure, Office 365 또는 Windows Intune을 통해 얻은 Azure AD 디렉터리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-109">You can use an Azure AD directory that you obtain through Microsoft Azure, Office 365, or Windows Intune.</span></span> <span data-ttu-id="0f649-110">이러한 항목이 두 개 이상 있는 경우 사용할 것을 결정하려면 [Azure AD 디렉터리 관리](active-directory-administer.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f649-110">If you have two or more of these, see [Administer your Azure AD directory](active-directory-administer.md) to determine which one to use.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f649-111">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-111">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="0f649-112">Azure AD 관리 센터에서 관리자 역할을 할당하는 방법은 [Azure Active Directory에서 관리자 역할 할당](active-directory-enterprise-apps-manage-sso.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f649-112">For how to assign administrator roles in the Azure AD admin center, see [Assigning administrator roles in Azure Active Directory](active-directory-enterprise-apps-manage-sso.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="0f649-113">인증</span><span class="sxs-lookup"><span data-stu-id="0f649-113">Authentication</span></span>
<span data-ttu-id="0f649-114">SAML 2.0, WS-Federation 또는 OpenID Connect 프로토콜을 지원하는 응용 프로그램의 경우 Azure Active Directory는 서명 인증서를 사용하여 트러스트 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-114">For applications that support the SAML 2.0, WS-Federation, or OpenID Connect protocols, Azure Active Directory uses signing certificates to establish trust relationships.</span></span> <span data-ttu-id="0f649-115">이에 대한 자세한 내용은 [페더레이션된 Single Sign-On에 대한 인증서 관리](active-directory-sso-certs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f649-115">For more information about this, see [Managing certificates for federated single sign-on](active-directory-sso-certs.md).</span></span>

<span data-ttu-id="0f649-116">HTML 폼 기반 로그인만 지원하는 응용 프로그램의 경우 Azure Active Directory는 ‘암호 보관'을 사용하여 트러스트 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-116">For applications that support only HTML forms-based sign-in, Azure Active Directory uses ‘password vaulting’ to establish trust relationships.</span></span> <span data-ttu-id="0f649-117">이에 따라 조직의 사용자가 SaaS 응용 프로그램에서 사용자 계정 정보를 사용하여 Azure AD에 의해 SaaS 응용 프로그램에 자동으로 로그인될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-117">This enables the users in your organization to be automatically signed in to a SaaS application by Azure AD using the user account information from the SaaS application.</span></span> <span data-ttu-id="0f649-118">Azure AD는 사용자 계정 정보 및 관련된 암호를 수집하고 안전하게 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-118">Azure AD collects and securely stores the user account information and the related password.</span></span> <span data-ttu-id="0f649-119">자세한 내용은 [암호 기반 Single Sign-On](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f649-119">For more information, see [Password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

## <a name="authorization"></a><span data-ttu-id="0f649-120">권한 부여</span><span class="sxs-lookup"><span data-stu-id="0f649-120">Authorization</span></span>
<span data-ttu-id="0f649-121">Single Sign-On을 통해 인증한 후에는 사용자에게 프로비전된 계정을 사용하여 응용 프로그램을 사용하도록 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-121">A provisioned account enables a user to be authorized to use an application after they have authenticated through single sign-on.</span></span> <span data-ttu-id="0f649-122">사용자 프로비저닝은 수동으로 수행할 수 있으며, Azure Active Directory에서 변경한 사항에 따라 SaaS 앱에서 사용자 정보를 추가하고 제거할 수 있는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-122">User provisioning can be done manually, or in some cases you can add and remove user information from the SaaS app based on changes made in Azure Active Directory.</span></span> <span data-ttu-id="0f649-123">자동화된 프로비저닝을 위해 기존 Azure AD 커넥터를 사용하는 방법에 대한 자세한 내용은 [SaaS 응용 프로그램에 대한 자동화된 사용자 프로비저닝 및 프로비저닝 해제](active-directory-saas-app-provisioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f649-123">For more information on using existing Azure AD connectors for automated provisioning, see  [Automated user provisioning and de-provisioning for SaaS applications](active-directory-saas-app-provisioning.md).</span></span>

<span data-ttu-id="0f649-124">또는 수동으로 사용자 정보를 앱에 추가하거나 마켓플레이스에서 사용할 수 있는 다른 프로비저닝 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-124">Otherwise, you can manually add user information to an app, or use other provisioning solutions that are available in the marketplace.</span></span>

## <a name="access"></a><span data-ttu-id="0f649-125">Access</span><span class="sxs-lookup"><span data-stu-id="0f649-125">Access</span></span>
<span data-ttu-id="0f649-126">Azure AD는 조직의 최종 사용자에게 응용 프로그램을 배포하는 여러 가지 사용자 지정 가능한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-126">Azure AD provides several customizable ways to deploy applications to end users in your organization.</span></span> <span data-ttu-id="0f649-127">특정 배포 또는 액세스 솔루션으로 제한되지 않으며,</span><span class="sxs-lookup"><span data-stu-id="0f649-127">You are not locked into any particular deployment or access solution.</span></span> <span data-ttu-id="0f649-128">[요구 사항에 가장 적합한 솔루션](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-128">You can use [the solution that best suits your needs](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

## <a name="additional-considerations-for-applications-already-in-use"></a><span data-ttu-id="0f649-129">이미 사용 중인 응용 프로그램에 대한 추가 고려 사항</span><span class="sxs-lookup"><span data-stu-id="0f649-129">Additional considerations for applications already in use</span></span>
<span data-ttu-id="0f649-130">조직이 사용하는 응용 프로그램에 Single Sign-On을 설치하는 작업은 새 응용 프로그램에 새 계정을 만드는 것과 다른 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-130">Setting up single sign on for an application that your organization already uses is a different process from the process of creating new accounts for a new application.</span></span> <span data-ttu-id="0f649-131">다음 몇 가지 준비 단계를 포함합니다. 응용 프로그램에서 Azure AD ID에 사용자 ID를 매핑하고 통합된 후에 사용자가 응용 프로그램에 로그인하는 방법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-131">There are a couple of preliminary steps including: mapping user identities in the application to Azure AD identities, and understanding how users will experience logging in to an application after it is integrated.</span></span>

> [!NOTE]
> <span data-ttu-id="0f649-132">기존 응용 프로그램에 대한 SSO를 설정하려면 Azure AD와 SaaS 응용 프로그램에서 전역 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-132">To set up SSO for an existing application, you need to have global administrator rights in both Azure AD and the SaaS application.</span></span>
>
>

### <a name="mapping-user-accounts"></a><span data-ttu-id="0f649-133">사용자 계정 매핑</span><span class="sxs-lookup"><span data-stu-id="0f649-133">Mapping user accounts</span></span>
<span data-ttu-id="0f649-134">사용자의 ID에는 일반적으로 전자 메일 주소 또는 사용자 계정 이름(UPN)일 수 있는 고유 식별자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-134">A user's identity typically has a unique identifier that could be an email address, or user principal name (UPN).</span></span> <span data-ttu-id="0f649-135">각 사용자의 응용 프로그램 ID를 해당 Azure AD ID에 링크(맵핑)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-135">You will need to link (map) each user's application identity to their respective Azure AD identity.</span></span> <span data-ttu-id="0f649-136">응용 프로그램 인증이 요구하는 방법에 따라 이 작업을 수행하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-136">There are a couple of ways to accomplish this depending on how the requirement of your application authentication.</span></span>

<span data-ttu-id="0f649-137">응용 프로그램 ID를 Azure AD ID와 매핑하는 방법에 대한 자세한 내용은 [SAML 토큰에서 발급된 클레임 사용자 지정](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) 및 [프로비전을 위한 특성 매핑 사용자 지정](active-directory-saas-customizing-attribute-mappings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f649-137">For more information about mapping application identities with Azure AD identities, see [Customizing claims issued in the SAML token](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) and [Customizing attribute mappings for provisioning](active-directory-saas-customizing-attribute-mappings.md).</span></span>

### <a name="understanding-the-users-log-in-experience"></a><span data-ttu-id="0f649-138">사용자의 로그인 환경 이해</span><span class="sxs-lookup"><span data-stu-id="0f649-138">Understanding the user's log in experience</span></span>
<span data-ttu-id="0f649-139">이미 사용 중인 응용 프로그램에 대한 SSO를 통합할 때 사용자 환경이 영향을 받게 된다는 사실을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-139">When you integrate SSO for an application that’s already in use, it’s important to realize that the user experience will be affected.</span></span> <span data-ttu-id="0f649-140">모든 응용 프로그램의 경우 사용자는 먼저 Azure AD 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-140">For all applications, users will start using their Azure AD credentials to sign in.</span></span> <span data-ttu-id="0f649-141">또한 다른 포털을 사용하여 응용 프로그램에 액세스해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-141">It could also be that they must use a different portal to access the applications.</span></span>

<span data-ttu-id="0f649-142">응용 프로그램에 따라 SSO가 응용 프로그램의 로그인 인터페이스에서 수행될 수도 있고, 사용자가 [내 앱](http://myapps.microsoft.com) 또는 [Office365](http://portal.office.com/myapps)와 같은 중앙 포털을 통해 로그인해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-142">SSO for some applications can be done on the application's sign in interface, but for other applications, the user will have to go through a central portal such as ([My Apps](http://myapps.microsoft.com) or [Office365](http://portal.office.com/myapps)) to sign in.</span></span> <span data-ttu-id="0f649-143">다양한 유형의 SSO 및 해당 사용자 환경에 대한 자세한 내용은 [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f649-143">Learn more about the different types of SSO and their user experiences in [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<span data-ttu-id="0f649-144">또 다른 중요한 리소스는 *개발자 가이드* 문서에 있는 [사용자 동의 억제](active-directory-applications-guiding-developers-for-lob-applications.md) 입니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-144">Another valuable resource is *Suppressing user consent* in the [Guiding developers](active-directory-applications-guiding-developers-for-lob-applications.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f649-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f649-145">Next steps</span></span>
<span data-ttu-id="0f649-146">앱 갤러리에서 찾은 SaaS 앱의 경우 Azure AD는 [SaaS 앱을 통합하는 방법에 대한 자습서](active-directory-saas-tutorial-list.md)를 다양하게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-146">For SaaS apps that you find in the App Gallery, Azure AD provides a number of [tutorials on how to integrate SaaS apps](active-directory-saas-tutorial-list.md).</span></span>

<span data-ttu-id="0f649-147">앱이 앱 갤러리에 없는 경우 [해당 앱을 사용자 지정 응용 프로그램으로 Azure AD 앱 갤러리에 추가](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-147">If app is not in App Gallery, you can [add it to the Azure AD App Gallery as a custom application](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).</span></span>

<span data-ttu-id="0f649-148">[Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)부터 시작하여 Azure.com 라이브러리에는 이러한 모든 문제에 대한 자세한 내용이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f649-148">There is much more detail on all of these issues in the Azure.com library, beginning with [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

<span data-ttu-id="0f649-149">또한 [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)를 놓치지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0f649-149">Plus, don't miss the [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md).</span></span>

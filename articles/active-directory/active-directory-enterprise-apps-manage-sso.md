---
title: "Azure Active Directory에서 엔터프라이즈 앱에 대한 Single Sign-On 관리 | Microsoft Docs"
description: "Azure Active Directory를 사용하여 엔터프라이즈 앱에 대한 Single Sign-On을 관리하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: c975428550690254ba989935fe5110c5903e7102
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a><span data-ttu-id="c0131-103">엔터프라이즈 앱에 대한 Single Sign-On 관리</span><span class="sxs-lookup"><span data-stu-id="c0131-103">Managing single sign-on for enterprise apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0131-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="c0131-104">Azure portal</span></span>](active-directory-enterprise-apps-manage-sso.md)
> * [<span data-ttu-id="c0131-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="c0131-105">Azure classic portal</span></span>](active-directory-sso-integrate-saas-apps.md)
> 

<span data-ttu-id="c0131-106">이 문서에서는 [Azure Portal](https://portal.azure.com)을 사용하여 엔터프라이즈 응용 프로그램에 대한 Single Sign-On 설정을 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-106">This article describes how to use the [Azure portal](https://portal.azure.com) to manage single sign-on settings for enterprise applications.</span></span> <span data-ttu-id="c0131-107">엔터프라이즈 앱은 조직 내에서 배포 및 사용되는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-107">Enterprise apps are apps that are deployed and used within your organization.</span></span> <span data-ttu-id="c0131-108">이 문서는 [Azure Active Directory 응용 프로그램 갤러리](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)에서 추가된 앱에 특별히 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-108">This article applies particularly to apps that were added from the [Azure Active Directory application gallery](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery).</span></span> 

## <a name="finding-your-apps-in-the-portal"></a><span data-ttu-id="c0131-109">포털에서 앱 찾기</span><span class="sxs-lookup"><span data-stu-id="c0131-109">Finding your apps in the portal</span></span>
<span data-ttu-id="c0131-110">Single Sign-On에 대해 설정되어 있는 모든 엔터프라이즈 앱은 Azure Portal에서 보고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-110">All enterprise apps that are set up for single sign-on can be viewed and managed in the Azure portal.</span></span> <span data-ttu-id="c0131-111">응용 프로그램은 포털의 **추가 서비스** &gt; **엔터프라이즈 응용 프로그램** 섹션에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-111">The applications can be found in the **More Services** &gt; **Enterprise Applications** section of the portal.</span></span> 

![엔터프라이즈 응용 프로그램 블레이드][1]

<span data-ttu-id="c0131-113">**모든 응용 프로그램**을 선택하여 구성된 모든 앱의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-113">Select **All applications** to view a list of all apps that have been configured.</span></span> <span data-ttu-id="c0131-114">앱을 선택하면 해당 앱의 리소스 블레이드를 로드하며 여기에서 해당 앱에 대한 보고서를 볼 수 있고 다양한 설정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-114">Selecting an app loads the resource blade for that app, where reports can be viewed for that app and a variety of settings can be managed.</span></span>

<span data-ttu-id="c0131-115">Single Sign-On 설정을 관리하려면 **Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-115">To manage single sign-on settings, select **Single sign-on**.</span></span>

![응용 프로그램 리소스 블레이드][2]

## <a name="single-sign-on-modes"></a><span data-ttu-id="c0131-117">Single Sign-On 모드</span><span class="sxs-lookup"><span data-stu-id="c0131-117">Single sign-on modes</span></span>
<span data-ttu-id="c0131-118">**Single Sign-On** 블레이드는 Single Sign-On 모드를 구성할 수 있는 **모드** 메뉴로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-118">The **Single sign-on** blade begins with a **Mode** menu, which allows the single sign-on mode to be configured.</span></span> <span data-ttu-id="c0131-119">사용 가능한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-119">The available options include:</span></span>

* <span data-ttu-id="c0131-120">**SAML 기반 로그온** - 이 옵션은 응용 프로그램이 SAML 2.0 프로토콜을 사용하여 Azure Active Directory로 전체 페더레이션된 Single Sign-On을 지원하는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-120">**SAML-based sign on** - This option is available if the application supports full federated single sign-on with Azure Active Directory using the SAML 2.0 protocol.</span></span>
* <span data-ttu-id="c0131-121">**암호 기반 로그온** - 이 옵션은 Azure AD가 이 응용 프로그램에 대해 입력하는 암호 양식을 지원하는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-121">**Password-based sign on** - This option is available if Azure AD supports password form filling for this application.</span></span>
* <span data-ttu-id="c0131-122">**연결된 로그온** - 이전에 "기존 Single Sign-On"이었던 이 옵션을 사용하면 관리자가 해당 사용자의 Azure AD 액세스 패널 또는 Office 365 응용 프로그램 시작 관리자에서 이 응용 프로그램에 대한 링크를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-122">**Linked sign on** - Formerly known as "Existing single sign-on", this option allows administrators to place a link to this application in their user's Azure AD Access Panel or Office 365 application launcher.</span></span>

<span data-ttu-id="c0131-123">이러한 모드에 대한 자세한 내용은 [Azure Active Directory에서 Single Sign-On이 작동하는 방식](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0131-123">For more information about these modes, see [How does single sign-on with Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="saml-based-sign-on"></a><span data-ttu-id="c0131-124">SAML 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="c0131-124">SAML-based sign-on</span></span>
<span data-ttu-id="c0131-125">**SAML 기반 로그온** 옵션을 선택하면 4개의 섹션으로 나뉘는 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-125">The **SAML-based sign on** option displays a blade that is divided in four sections:</span></span>

### <a name="domains-and-urls"></a><span data-ttu-id="c0131-126">도메인 및 URL</span><span class="sxs-lookup"><span data-stu-id="c0131-126">Domains and URLs</span></span>
<span data-ttu-id="c0131-127">여기에서 응용 프로그램의 도메인 및 URL에 대한 모든 세부 정보가 Azure AD 디렉터리에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-127">This is where all details about the application's domain and URLs are added to your Azure AD directory.</span></span> <span data-ttu-id="c0131-128">Single Sign-On 작업 앱을 만드는 데 필요한 모든 입력이 화면에 직접 표시되지만 모든 선택 사항 입력은 **Show advanced URL settings** (고급 URL 설정 표시) 확인란을 선택하여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-128">All inputs required to make single sign-on work app are displayed directly on the screen, whereas all optional inputs can be viewed by selecting the **Show advanced URL settings** checkbox.</span></span> <span data-ttu-id="c0131-129">지원되는 입력의 전체 목록에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-129">The full list of supported inputs includes:</span></span>

* <span data-ttu-id="c0131-130">**로그온 URL** – 사용자가 이 응용 프로그램에 로그인하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-130">**Sign On URL** – Where the user goes to sign-in to this application.</span></span> <span data-ttu-id="c0131-131">응용 프로그램이 서비스 공급자에서 시작된 Single Sign-On을 수행하도록 구성되면 사용자가 이 URL로 이동할 경우 서비스 공급자는 Azure AD를 인증하고 사용자에게 로그온하는 데 필요한 리디렉션을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-131">If the application is configured to perform service provider-initiated single sign on, then when a user navigates to this URL, the service provider does the necessary redirection to Azure AD to authenticate and sign the user in.</span></span> <span data-ttu-id="c0131-132">이 필드가 채워지면 Azure AD는 이 URL을 사용하여 Office 365 및 Azure AD 액세스 패널에서 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-132">If this field is populated, then Azure AD will use this URL to launch the application from Office 365 and the Azure AD Access Panel.</span></span> <span data-ttu-id="c0131-133">이 필드가 생략되면 해당 앱이 Office 365, Azure AD 액세스 패널 또는 Azure AD Single Sign-On URL에서 시작할 경우 Azure AD는 ID 공급자에서 시작된 로그인을 대신 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-133">If this field is omitted, then Azure AD instead performs identity provider -initiated sign on when the app is launched from Office 365, the Azure AD Access Panel, or from the Azure AD single sign-on URL.</span></span>
* <span data-ttu-id="c0131-134">**식별자** - 이 URI는 구성될 Single Sign-On에 대해 응용 프로그램을 고유하게 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-134">**Identifier** - This URI should uniquely identify the application for which single sign on is being configured.</span></span> <span data-ttu-id="c0131-135">이는 Azure AD가 SAML 토큰의 대상 매개 변수로서 응용 프로그램에 다시 전송하는 값이며, 응용 프로그램의 유효성을 검사하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-135">This is the value that Azure AD sends back to application as the Audience parameter of the SAML token, and the application is expected to validate it.</span></span> <span data-ttu-id="c0131-136">또한 이 값은 응용 프로그램에서 제공하는 모든 SAML 메타데이터 내에서 엔터티 ID로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-136">This value also appears as the Entity ID in any SAML metadata provided by the application.</span></span>
* <span data-ttu-id="c0131-137">**회신 URL** - 회신 URL은 응용 프로그램이 SAML 토큰을 수신해야 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-137">**Reply URL** - The reply URL is where the application expects to receive the SAML token.</span></span> <span data-ttu-id="c0131-138">이 URL은 ACS(Assertion Consumer Service) URL이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-138">This is also referred to as the Assertion Consumer Service (ACS) URL.</span></span> <span data-ttu-id="c0131-139">이러한 내용을 입력한 후에 다음을 클릭하여 다음 화면으로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-139">After these have been entered, click Next to proceed to the next screen.</span></span> <span data-ttu-id="c0131-140">이 화면은 응용 프로그램쪽에서 구성되어야 하는 사항에 대한 정보를 제공하여 Azure AD에서 SAML 토큰을 수락하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-140">This screen provides information about what needs to be configured on the application side to enable it to accept a SAML token from Azure AD.</span></span>
* <span data-ttu-id="c0131-141">**릴레이 상태** - 릴레이 상태는 인증이 완료된 후 사용자를 리디렉션할 위치를 응용 프로그램에 알릴 수 있는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-141">**Relay State** -  The relay state is an optional parameter that can help tell the application where to redirect the user after authentication is completed.</span></span> <span data-ttu-id="c0131-142">일반적으로 해당 값은 응용 프로그램에서 올바른 URL이지만 일부 응용 프로그램은 이 필드를 다르게 사용합니다(자세한 내용은 앱의 Single Sign-On 설명서 참조).</span><span class="sxs-lookup"><span data-stu-id="c0131-142">Typically the value is a valid URL at the application, however some applications use this field differently (see the app's single sign on documentation for details).</span></span> <span data-ttu-id="c0131-143">릴레이 상태를 설정하는 기능은 새 Azure Portal에 고유한 새 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-143">The ability to set the relay state is a new feature that is unique to the new Azure portal.</span></span>

### <a name="user-attributes"></a><span data-ttu-id="c0131-144">사용자 특성</span><span class="sxs-lookup"><span data-stu-id="c0131-144">User Attributes</span></span>
<span data-ttu-id="c0131-145">여기에서 관리자는 사용자 로그인마다 Azure AD가 응용 프로그램에 발행하는 SAML 토큰에서 전송되는 특성을 보고 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-145">This is where admins can view and edit the attributes that are sent in the SAML token that Azure AD issues to the application each time users sign in.</span></span>

<span data-ttu-id="c0131-146">편집 가능하며 지원되는 유일한 특성은 **사용자 ID** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-146">The only editable attribute supported is the **User Identifier** attribute.</span></span> <span data-ttu-id="c0131-147">이 특성의 값은 응용 프로그램 내에서 각 사용자를 고유하게 식별하는 Azure AD의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-147">The value of this attribute is the field in Azure AD that uniquely identifies each user within the application.</span></span> <span data-ttu-id="c0131-148">예를 들어 "메일 주소"를 사용자 이름 및 고유 식별자로 사용하여 앱이 배포된 경우 해당 값은 Azure AD의 "user.mail" 필드로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-148">For example, if the app was deployed using the "Email address" as the username and unique identifier, then the value would be set to the "user.mail" field in Azure AD.</span></span>

### <a name="saml-signing-certificate"></a><span data-ttu-id="c0131-149">SAML 서명 인증서</span><span class="sxs-lookup"><span data-stu-id="c0131-149">SAML Signing Certificate</span></span>
<span data-ttu-id="c0131-150">이 섹션에서는 Azure AD가 사용자 인증마다 응용 프로그램에 발급된 SAML 토큰을 서명하는 데 사용하는 인증서의 세부 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-150">This section shows the details of the certificate that Azure AD uses to sign the SAML tokens that are issued to the application each time the user authenticates.</span></span> <span data-ttu-id="c0131-151">이를 통해 만료 날짜를 포함하여 현재 인증서의 속성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-151">It allows the properties of the current certificate to be inspected, including the expiration date.</span></span>

### <a name="application-configuration"></a><span data-ttu-id="c0131-152">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="c0131-152">Application Configuration</span></span>
<span data-ttu-id="c0131-153">마지막 섹션에서는 Azure Active Directory를 ID 공급자로 사용하도록 응용 프로그램 자체를 구성하는 데 필요한 설명서 및/또는 컨트롤을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-153">The final section provides the documentation and/or controls required to configure the application itself to use Azure Active Directory as an identity provider.</span></span>

<span data-ttu-id="c0131-154">**응용 프로그램 구성** 플라이아웃 메뉴에서 응용 프로그램을 구성하기 위해 포함된 간결한 새 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-154">The **Configure Application** fly-out menu provides new concise, embedded instructions for configuring the application.</span></span> <span data-ttu-id="c0131-155">이는 새 Azure Portal에 고유한 또 다른 새 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-155">This is another new feature unique to the new Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="c0131-156">포함된 설명서의 전체 예제를 보려면 Salesforce.com 응용 프로그램을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0131-156">For a complete example of embedded documentation, see the Salesforce.com application.</span></span> <span data-ttu-id="c0131-157">추가 앱에 대한 설명서는 계속 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-157">Documentation for additional apps is being continually added.</span></span>
> 
> 

![포함된 문서][3]

## <a name="password-based-sign-on"></a><span data-ttu-id="c0131-159">암호 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="c0131-159">Password-based sign on</span></span>
<span data-ttu-id="c0131-160">응용 프로그램을 지원하는 경우 암호 기반 SSO 모드를 선택하고 **저장** 을 선택하면 즉시 구성되어 암호 기반 SSO를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-160">If supported for the application, selecting the password-based SSO mode and selecting **Save** instantly configures it to do password-based SSO.</span></span> <span data-ttu-id="c0131-161">암호 기반 SSO를 배포하는 방법은 [Azure Active Directory에서 Single Sign-On이 작동하는 방식](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0131-161">For more information about deploying password-based SSO, see [How does single sign-on with Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

![암호 기반 로그온][4]

## <a name="linked-sign-on"></a><span data-ttu-id="c0131-163">연결된 로그온</span><span class="sxs-lookup"><span data-stu-id="c0131-163">Linked sign on</span></span>
<span data-ttu-id="c0131-164">응용 프로그램을 지원하는 경우 연결된 SSO 모드를 선택하면 사용자가 이 앱을 클릭할 때 Azure AD 액세스 패널 또는 Office 365가 리디렉션하는 URL을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-164">If supported for the application, selecting the linked SSO mode allows you to enter the URL that you want the Azure AD Access Panel or Office 365 to redirect to when users click on this app.</span></span> <span data-ttu-id="c0131-165">연결된 SSO(이전의 "기존 SSO")에 대한 자세한 내용은 [Azure Active Directory에서 Single Sign-On이 작동하는 방식](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0131-165">For more information about linked SSO (formerly known as "existing SSO"), see [How does single sign-on with Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

![연결된 로그온][5]

##<a name="feedback"></a><span data-ttu-id="c0131-167">사용자 의견</span><span class="sxs-lookup"><span data-stu-id="c0131-167">Feedback</span></span>

<span data-ttu-id="c0131-168">향상된 Azure AD 환경 사용이 사용자의 마음에 들기를 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-168">We hope you like using the improved Azure AD experience.</span></span> <span data-ttu-id="c0131-169">사용자 의견을 계속 보내주세요!</span><span class="sxs-lookup"><span data-stu-id="c0131-169">Please keep the feedback coming!</span></span> <span data-ttu-id="c0131-170">[피드백 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal)의 **관리자 포털Admin Portal** 섹션에서 개선을 위한 의견과 아이디어를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-170">Post your feedback and ideas for improvement in the **Admin Portal** section of our [feedback forum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span></span>  <span data-ttu-id="c0131-171">매일 멋진 새로운 기능을 구축하는 방법을 기대하며, 사용자의 지침에 따라 다음에 구축할 기능을 구체화하고 정의하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c0131-171">We’re excited about building cool new stuff every day, and use your guidance to shape and define what we build next.</span></span>

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG

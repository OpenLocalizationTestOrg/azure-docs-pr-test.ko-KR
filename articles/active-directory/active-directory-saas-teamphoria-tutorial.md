---
title: "자습서: Teamphoria와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Teamphoria 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 2a35efb04d7fe22abc6894c149caf090666ce016
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="e8c01-103">자습서: Teamphoria와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="e8c01-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="e8c01-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Teamphoria를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8c01-105">Teamphoria를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e8c01-106">Teamphoria에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-106">You can control in Azure AD who has access to Teamphoria</span></span>
- <span data-ttu-id="e8c01-107">사용자가 해당 Azure AD 계정으로 Teamphoria에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e8c01-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="e8c01-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c01-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Teamphoria, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="e8c01-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e8c01-110">Prerequisites</span></span>

<span data-ttu-id="e8c01-111">Teamphoria와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-111">To configure Azure AD integration with Teamphoria, you need the following items:</span></span>

- <span data-ttu-id="e8c01-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="e8c01-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8c01-113">Teamphoria Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="e8c01-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8c01-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8c01-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8c01-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e8c01-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8c01-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="e8c01-118">Scenario description</span></span>
<span data-ttu-id="e8c01-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8c01-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8c01-121">갤러리에서 Teamphoria 추가</span><span class="sxs-lookup"><span data-stu-id="e8c01-121">Adding Teamphoria from the gallery</span></span>
2. <span data-ttu-id="e8c01-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e8c01-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-the-gallery"></a><span data-ttu-id="e8c01-123">갤러리에서 Teamphoria 추가</span><span class="sxs-lookup"><span data-stu-id="e8c01-123">Adding Teamphoria from the gallery</span></span>
<span data-ttu-id="e8c01-124">Teamphoria의 Azure AD 통합을 구성하려면 갤러리의 Teamphoria를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e8c01-125">**갤러리에서 Teamphoria를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e8c01-125">**To add Teamphoria from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e8c01-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e8c01-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e8c01-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="e8c01-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="e8c01-133">검색 상자에 **Teamphoria**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-133">In the search box, type **Teamphoria**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="e8c01-135">결과 창에서 **Teamphoria**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e8c01-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e8c01-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e8c01-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Teamphoria에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e8c01-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Teamphoria 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span></span> <span data-ttu-id="e8c01-140">즉, Azure AD 사용자와 Teamphoria의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span></span>

<span data-ttu-id="e8c01-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Teamphoria의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamphoria.</span></span>

<span data-ttu-id="e8c01-142">Teamphoria에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-142">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e8c01-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e8c01-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8c01-145">**[Teamphoria 테스트 사용자 만들기](#creating-a-teamphoria-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Teamphoria에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e8c01-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8c01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e8c01-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="e8c01-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e8c01-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Teamphoria 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="e8c01-150">**Teamphoria에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e8c01-150">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="e8c01-151">Azure 관리 포털의 **Teamphoria** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-151">In the Azure Management portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="e8c01-153">**Single sign on** 대화 상자에서 **모드**로 **SAML 기반 로그온**을 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="e8c01-155">**Teamphoria 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-155">On the **Teamphoria Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="e8c01-157">a.</span><span class="sxs-lookup"><span data-stu-id="e8c01-157">a.</span></span> <span data-ttu-id="e8c01-158">**로그온 URL** 텍스트 상자에서 `https://<sub-domain>.teamphoria.com/login` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-158">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="e8c01-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-159">Please note that these are not the real values.</span></span> <span data-ttu-id="e8c01-160">이러한 값을 실제 로그온 URL로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-160">You have to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="e8c01-161">로그온 URL을 가져오려면 [Teamphoria 클라이언트 지원 팀](https://www.teamphoria.com/)에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span></span> 

4. <span data-ttu-id="e8c01-162">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="e8c01-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-164">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e8c01-166">**Teamphoria 구성** 섹션에서 **Teamphoria 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-166">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e8c01-167">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="e8c01-169">**Teamphoria** 측에서 Single Sign-On을 구성하려면 관리자 권한으로 Teamphoria 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-169">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="e8c01-170">왼쪽 도구 모음에서 **관리 설정** 옵션으로 이동하고 구성 탭 아래에서 **SINGLE SIGN-ON**을 클릭하여 SSO 구성 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-170">Go to **ADMIN SETTINGS** option in the left toolbar and under the the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="e8c01-172">오른쪽 위 모서리에서 **새 ID 공급자 추가** 옵션을 클릭하여 SSO에 대한 설정을 추가하기 위한 양식을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-172">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="e8c01-174">아래에서 설명한 대로 필드에 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-174">Enter the details in the fields as described below-</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="e8c01-176">a.</span><span class="sxs-lookup"><span data-stu-id="e8c01-176">a.</span></span> <span data-ttu-id="e8c01-177">**표시 이름**: 관리 페이지에서 플러그 인의 표시 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-177">**DISPLAY NAME** : Enter the display name of the plugin on the admin page.</span></span>

    <span data-ttu-id="e8c01-178">b.</span><span class="sxs-lookup"><span data-stu-id="e8c01-178">b.</span></span> <span data-ttu-id="e8c01-179">**단추 이름**: SSO를 통한 로그인에 대해 로그인 페이지에 표시하는 탭의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-179">**BUTTON NAME** : The name of the tab which will display on the login page for logging in via SSO.</span></span>

    <span data-ttu-id="e8c01-180">c.</span><span class="sxs-lookup"><span data-stu-id="e8c01-180">c.</span></span> <span data-ttu-id="e8c01-181">**인증서**: 메모장에서 Azure Portal에서 이전에 다운로드한 인증서를 열고 동일한 내용을 복사하고 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-181">**CERTIFICATE** : Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span></span>

    <span data-ttu-id="e8c01-182">d.</span><span class="sxs-lookup"><span data-stu-id="e8c01-182">d.</span></span> <span data-ttu-id="e8c01-183">**진입점**: Azure Portal에서 이전에 복사한 **SAML Single Sign-On 서비스 URL**을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-183">**ENTRY POINT** : Paste the **SAML Single Sign-On Service URL** copied earlier form the Azure portal.</span></span>

    <span data-ttu-id="e8c01-184">e.</span><span class="sxs-lookup"><span data-stu-id="e8c01-184">e.</span></span> <span data-ttu-id="e8c01-185">옵션을 **ON**으로 전환하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-185">Switch the option to **ON** and click on **SAVE**.</span></span>   

<!--### Next steps

To ensure users can sign-in to Teamphoria after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Teamphoria in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e8c01-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e8c01-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="e8c01-187">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-187">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="e8c01-189">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="e8c01-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e8c01-190">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-190">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e8c01-192">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-192">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e8c01-194">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-194">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e8c01-196">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e8c01-198">a.</span><span class="sxs-lookup"><span data-stu-id="e8c01-198">a.</span></span> <span data-ttu-id="e8c01-199">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8c01-200">b.</span><span class="sxs-lookup"><span data-stu-id="e8c01-200">b.</span></span> <span data-ttu-id="e8c01-201">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e8c01-202">c.</span><span class="sxs-lookup"><span data-stu-id="e8c01-202">c.</span></span> <span data-ttu-id="e8c01-203">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e8c01-204">d.</span><span class="sxs-lookup"><span data-stu-id="e8c01-204">d.</span></span> <span data-ttu-id="e8c01-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="e8c01-206">Teamphoria 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e8c01-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="e8c01-207">Azure AD 사용자가 Teamphoria에 로그인할 수 있도록 하려면 Teamphoria로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-207">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="e8c01-208">Teamphoria의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-208">In the case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="e8c01-209">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e8c01-209">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="e8c01-210">Teamphoria 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-210">Log in to your Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="e8c01-211">왼쪽 도구 모음에서 **관리자** 설정을 클릭하고 **관리** 탭 아래에서 **사용자**를 클릭하여 사용자에 대한 관리 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-211">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span></span>

    ![직원 추가](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="e8c01-213">**수동 초대** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-213">Click on the **MANUAL INVITE** option.</span></span>

    ![피플 초대](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="e8c01-215">이 페이지에서 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-215">On this page, perform following action.</span></span> 
    
    ![피플 초대](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="e8c01-217">a.</span><span class="sxs-lookup"><span data-stu-id="e8c01-217">a.</span></span> <span data-ttu-id="e8c01-218">**전자 메일 주소** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-218">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e8c01-219">b.</span><span class="sxs-lookup"><span data-stu-id="e8c01-219">b.</span></span> <span data-ttu-id="e8c01-220">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-220">In the **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="e8c01-221">c.</span><span class="sxs-lookup"><span data-stu-id="e8c01-221">c.</span></span> <span data-ttu-id="e8c01-222">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-222">In the **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="e8c01-223">d.</span><span class="sxs-lookup"><span data-stu-id="e8c01-223">d.</span></span> <span data-ttu-id="e8c01-224">**1 사용자 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="e8c01-225">사용자는 시스템에서 생성할 초대를 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-225">User needs to accept the invite to get created in the system.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e8c01-226">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="e8c01-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e8c01-227">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Teamphoria에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-227">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamphoria.</span></span>

![사용자 할당][200] 

<span data-ttu-id="e8c01-229">**Britta Simon을 Teamphoria에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="e8c01-229">**To assign Britta Simon to Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="e8c01-230">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-230">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="e8c01-232">응용 프로그램 목록에서 **Teamphoria**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-232">In the applications list, select **Teamphoria**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="e8c01-234">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-234">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="e8c01-236">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-236">Click **Add** button.</span></span> <span data-ttu-id="e8c01-237">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="e8c01-239">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e8c01-240">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8c01-241">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e8c01-242">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="e8c01-242">Testing single sign-on</span></span>

<span data-ttu-id="e8c01-243">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e8c01-244">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8c01-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="e8c01-245">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c01-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e8c01-246">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e8c01-246">Additional resources</span></span>

* [<span data-ttu-id="e8c01-247">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="e8c01-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8c01-248">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e8c01-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png


---
title: "자습서: Procore SSO와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Procore SSO 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 042a41eaa6bb21670b4c12068f1b017222f64b99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="ef02c-103">자습서: Procore SSO와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="ef02c-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="ef02c-104">이 자습서에서는 Procore SSO를 Azure AD(Azure Active Directory)와 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-104">In this tutorial, you learn how to integrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ef02c-105">Procore SSO를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-105">Integrating Procore SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ef02c-106">Procore SSO에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-106">You can control in Azure AD who has access to Procore SSO</span></span>
- <span data-ttu-id="ef02c-107">사용자의 Azure AD 계정으로 Procore SSO(Single Sign-on)에 자동으로 로그온되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-107">You can enable your users to automatically get signed-on to Procore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ef02c-108">단일 중앙 위치인 Azure 관리 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="ef02c-109">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef02c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Procore SSO, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="ef02c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ef02c-110">Prerequisites</span></span>

<span data-ttu-id="ef02c-111">Procore SSO와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-111">To configure Azure AD integration with Procore SSO, you need the following items:</span></span>

- <span data-ttu-id="ef02c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="ef02c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ef02c-113">Procore SSO Single Sign-On을 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="ef02c-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ef02c-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ef02c-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ef02c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ef02c-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ef02c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="ef02c-118">Scenario description</span></span>
<span data-ttu-id="ef02c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ef02c-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ef02c-121">갤러리에서 Procore SSO 추가</span><span class="sxs-lookup"><span data-stu-id="ef02c-121">Adding Procore SSO from the gallery</span></span>
2. <span data-ttu-id="ef02c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ef02c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-the-gallery"></a><span data-ttu-id="ef02c-123">갤러리에서 Procore SSO 추가</span><span class="sxs-lookup"><span data-stu-id="ef02c-123">Adding Procore SSO from the gallery</span></span>
<span data-ttu-id="ef02c-124">Procore SSO가 Azure AD로 통합되도록 구성하려면 Procore SSO를 갤러리에서 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-124">To configure the integration of Procore SSO into Azure AD, you need to add Procore SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ef02c-125">**갤러리에서 Procore SSO를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ef02c-125">**To add Procore SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ef02c-126">**[Azure 관리 포털](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ef02c-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ef02c-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="ef02c-131">대화 상자 위쪽에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-131">Click **Add** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="ef02c-133">검색 상자에 **Procore SSO**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-133">In the search box, type **Procore SSO**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="ef02c-135">결과 창에서 **Procore SSO**를 선택하고 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-135">In the results panel, select **Procore SSO**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ef02c-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ef02c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ef02c-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Procore SSO에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ef02c-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Procore SSO 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Procore SSO is to a user in Azure AD.</span></span> <span data-ttu-id="ef02c-140">즉, Azure AD 사용자와 Procore SSO의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-140">In other words, a link relationship between an Azure AD user and the related user in Procore SSO needs to be established.</span></span>

<span data-ttu-id="ef02c-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Procore SSO의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Procore SSO.</span></span>

<span data-ttu-id="ef02c-142">Procore SSO에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-142">To configure and test Azure AD single sign-on with Procore SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ef02c-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ef02c-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ef02c-145">**[Procore SSO 테스트 사용자 만들기](#creating-a-procore-sso-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Procore SSO에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - to have a counterpart of Britta Simon in Procore SSO that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ef02c-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ef02c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ef02c-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="ef02c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ef02c-149">이 섹션에서는 Azure 관리 포털에서 Azure AD Single Sign-On을 사용하도록 설정하고 Procore SSO 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="ef02c-150">**Procore SSO에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ef02c-150">**To configure Azure AD single sign-on with Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="ef02c-151">Azure 관리 포털의 **Procore SSO** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-151">In the Azure Management portal, on the **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="ef02c-153">**Single sign on** 대화 상자에서 **SAML 기반 로그인**으로 **모드**를 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Single Sign-On 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="ef02c-155">**Procore SSO 도메인 및 URL** 섹션에서 앱이 Azure와 이미 사전 통합되었으므로 사용자는 아무 단계도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-155">On the **Procore SSO Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="ef02c-157">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="ef02c-159">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-159">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ef02c-161">**Procore SSO 구성** 섹션에서 **Procore SSO 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-161">On the **Procore SSO Configuration** section, click **Configure Procore SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ef02c-162">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-162">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="ef02c-164">**Procore SSO** 측에서 Single Sign-On을 구성하려면 Procore 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-164">To configure single sign-on on **Procore SSO** side, login to your procore company site as an administrator.</span></span>

8. <span data-ttu-id="ef02c-165">도구 상자 드롭다운에서 **관리**를 클릭하여 SSO 설정 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-165">From the toolbox drop down, click on **Admin** to open the SSO settings page.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="ef02c-167">아래 설명에 따라 값을 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-167">Paste the values in the boxes as described below-</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="ef02c-169">a.</span><span class="sxs-lookup"><span data-stu-id="ef02c-169">a.</span></span> <span data-ttu-id="ef02c-170">**Single Sign-On 발급자 URL** 상자에 Azure Portal에서 복사한 SAML 엔터티 ID를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-170">In the **Single Sign On Issuer URL** box, paste the SAML Entity ID copied from the Azure portal.</span></span>

    <span data-ttu-id="ef02c-171">b.</span><span class="sxs-lookup"><span data-stu-id="ef02c-171">b.</span></span> <span data-ttu-id="ef02c-172">**SAML 로그온 대상 URL** 상자에 Azure Portal에서 복사한 SAML Single Sign-On 서비스 URL을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-172">In the **SAML Sign On Target URL** box, paste the SAML Single Sign-On Service URL copied from the Azure portal.</span></span>

    <span data-ttu-id="ef02c-173">c.</span><span class="sxs-lookup"><span data-stu-id="ef02c-173">c.</span></span> <span data-ttu-id="ef02c-174">이제 앞에서 Azure Portal에서 다운로드한 **메타데이터 XML**을 열고 **X509Certificate**라는 태그에서 인증서를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-174">Now open the **Metadata XML** downloaded above from the Azure portal and copy the certficate in the tag named **X509Certificate**.</span></span> <span data-ttu-id="ef02c-175">복사한 값을 **Single Sign-On x509 인증서** 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-175">Paste the copied value into the **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="ef02c-176">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="ef02c-177">이러한 설정 후에 Procore에 로그인할 때 사용한 **도메인 이름**(예: **contoso.com**)을 [Procore 지원 팀](https://support.procore.com/)에 보내서 해당 도메인에 대해 페더레이션된 SSO를 활성화하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-177">After these settings, you needs to send the **domain name** (e.g **contoso.com**) through which you are logging into Procore to the [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

To ensure users can sign-in to Procore SSO after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Procore SSO in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ef02c-178">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ef02c-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="ef02c-179">이 섹션의 목적은 Azure 관리 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="ef02c-181">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="ef02c-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ef02c-182">**Azure 관리 포털**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ef02c-184">**사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭하여 사용자 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ef02c-186">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ef02c-188">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ef02c-190">a.</span><span class="sxs-lookup"><span data-stu-id="ef02c-190">a.</span></span> <span data-ttu-id="ef02c-191">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ef02c-192">b.</span><span class="sxs-lookup"><span data-stu-id="ef02c-192">b.</span></span> <span data-ttu-id="ef02c-193">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ef02c-194">c.</span><span class="sxs-lookup"><span data-stu-id="ef02c-194">c.</span></span> <span data-ttu-id="ef02c-195">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ef02c-196">d.</span><span class="sxs-lookup"><span data-stu-id="ef02c-196">d.</span></span> <span data-ttu-id="ef02c-197">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="ef02c-198">Procore SSO 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ef02c-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="ef02c-199">Procore 측에서 Procore 테스트 사용자를 만들려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="ef02c-199">Please follow the below steps to create a Procore test user on their side.</span></span>

1. <span data-ttu-id="ef02c-200">Procore 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-200">Login to your procore company site as an administrator.</span></span>  

2. <span data-ttu-id="ef02c-201">도구 상자 드롭다운에서 **디렉터리**를 클릭하여 회사 디렉터리 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-201">From the toolbox drop down, click on **Directory** to open the company directory page.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="ef02c-203">**Add a Person**(사람 추가) 옵션을 클릭하여 양식을 열고 다음 옵션을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-203">Click on **Add a Person** option to open the form and enter perform following options -</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="ef02c-205">a.</span><span class="sxs-lookup"><span data-stu-id="ef02c-205">a.</span></span> <span data-ttu-id="ef02c-206">**이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-206">In the **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="ef02c-207">b.</span><span class="sxs-lookup"><span data-stu-id="ef02c-207">b.</span></span> <span data-ttu-id="ef02c-208">**성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-208">In the **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="ef02c-209">c.</span><span class="sxs-lookup"><span data-stu-id="ef02c-209">c.</span></span> <span data-ttu-id="ef02c-210">**전자 메일 주소** 텍스트 상자에 사용자의 전자 메일 주소(예: **BrittaSimon@contoso.com**)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-210">In the **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="ef02c-211">d.</span><span class="sxs-lookup"><span data-stu-id="ef02c-211">d.</span></span> <span data-ttu-id="ef02c-212">**Permission Template**(권한 템플릿)에 **Apply Permission Template Later**(권한 템플릿 나중에 적용)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="ef02c-213">e.</span><span class="sxs-lookup"><span data-stu-id="ef02c-213">e.</span></span> <span data-ttu-id="ef02c-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-214">Click **Create**.</span></span>

4. <span data-ttu-id="ef02c-215">새로 추가된 연락처에 대한 세부 정보를 확인하고 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-215">Check and update the details for the newly added contact.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="ef02c-217">**Save and Send Invitiation**(저장 및 초대 보내기)(메일을 통한 초대가 필요한 경우) 또는 **저장**(바로 저장)을 클릭하여 사용자 등록을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) to complete the user registration.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ef02c-219">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="ef02c-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ef02c-220">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Procore SSO에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Procore SSO.</span></span>

![사용자 할당][200] 

<span data-ttu-id="ef02c-222">**Britta Simon을 Procore SSO에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ef02c-222">**To assign Britta Simon to Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="ef02c-223">Azure 관리 포털에서 응용 프로그램 보기를 열고 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="ef02c-225">응용 프로그램 목록에서 **Procore SSO**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-225">In the applications list, select **Procore SSO**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="ef02c-227">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-227">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="ef02c-229">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-229">Click **Add** button.</span></span> <span data-ttu-id="ef02c-230">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="ef02c-232">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ef02c-233">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ef02c-234">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ef02c-235">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="ef02c-235">Testing single sign-on</span></span>

<span data-ttu-id="ef02c-236">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ef02c-237">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ef02c-238">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef02c-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="ef02c-239">액세스 패널에서 Procore SSO 타일을 클릭하면 Procore SSO 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef02c-239">When you click the Procore SSO tile in the Access Panel, you should get automatically signed-on to your Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ef02c-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ef02c-240">Additional resources</span></span>

* [<span data-ttu-id="ef02c-241">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="ef02c-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ef02c-242">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ef02c-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png


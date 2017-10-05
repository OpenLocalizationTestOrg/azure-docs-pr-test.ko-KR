---
title: "자습서: Adaptive Suite와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Abintegro 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 5d7ba2f4c7d814e3aaa1bf804ddc5030380ccb2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="b6c66-103">자습서: Adaptive Suite와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b6c66-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="b6c66-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Adaptive Suite를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-104">In this tutorial, you learn how to integrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b6c66-105">Adaptive Suite를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-105">Integrating Adaptive Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b6c66-106">Adaptive Suite에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-106">You can control in Azure AD who has access to Adaptive Suite</span></span>
- <span data-ttu-id="b6c66-107">사용자가 Azure AD 계정으로 Adaptive Suite에 자동으로 로그온(Single Sign-on)할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-107">You can enable your users to automatically get signed-on to Adaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b6c66-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b6c66-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6c66-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6c66-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b6c66-110">Prerequisites</span></span>

<span data-ttu-id="b6c66-111">Adaptive Suite와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-111">To configure Azure AD integration with Adaptive Suite, you need the following items:</span></span>

- <span data-ttu-id="b6c66-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b6c66-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b6c66-113">Adaptive Suite Single-Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b6c66-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b6c66-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b6c66-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b6c66-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b6c66-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b6c66-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b6c66-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b6c66-118">Scenario description</span></span>
<span data-ttu-id="b6c66-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b6c66-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b6c66-121">갤러리에서 Adaptive Suite 추가</span><span class="sxs-lookup"><span data-stu-id="b6c66-121">Adding Adaptive Suite from the gallery</span></span>
2. <span data-ttu-id="b6c66-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b6c66-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-the-gallery"></a><span data-ttu-id="b6c66-123">갤러리에서 Adaptive Suite 추가</span><span class="sxs-lookup"><span data-stu-id="b6c66-123">Adding Adaptive Suite from the gallery</span></span>
<span data-ttu-id="b6c66-124">Adaptive Suite가 Azure AD에 통합되도록 구성하려면 갤러리의 Adaptive Suite를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-124">To configure the integration of Adaptive Suite into Azure AD, you need to add Adaptive Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b6c66-125">**갤러리에서 Adaptive Suite를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b6c66-125">**To add Adaptive Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b6c66-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b6c66-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b6c66-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b6c66-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b6c66-133">검색 상자에 **Adaptive Suite**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-133">In the search box, type **Adaptive Suite**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="b6c66-135">결과 창에서 **Adaptive Suite**를 선택한 다음 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-135">In the results panel, select **Adaptive Suite**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b6c66-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b6c66-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b6c66-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Adaptive Suite에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b6c66-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Adaptive Suite 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adaptive Suite is to a user in Azure AD.</span></span> <span data-ttu-id="b6c66-140">즉, Azure AD 사용자와 Adaptive Suite의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-140">In other words, a link relationship between an Azure AD user and the related user in Adaptive Suite needs to be established.</span></span>

<span data-ttu-id="b6c66-141">Adaptive Suite에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-141">In Adaptive Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b6c66-142">Adaptive Suite에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-142">To configure and test Azure AD single sign-on with Adaptive Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b6c66-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b6c66-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b6c66-145">**[Adaptive Suite 테스트 사용자 만들기](#creating-an-adaptive-suite-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Adaptive Suite에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - to have a counterpart of Britta Simon in Adaptive Suite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b6c66-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b6c66-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b6c66-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b6c66-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b6c66-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Adaptive Suite 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="b6c66-150">**Adaptive Suite에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b6c66-150">**To configure Azure AD single sign-on with Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="b6c66-151">Azure Portal의 **Adaptive Suite** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-151">In the Azure portal, on the **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b6c66-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="b6c66-155">**Adaptive Suite 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-155">On the **Adaptive Suite Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="b6c66-157">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="b6c66-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="b6c66-158">Adaptive Suite의 **SAML SSO 설정** 페이지에서 이 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-158">You can get this value from the Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="b6c66-159">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="b6c66-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-161">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b6c66-163">**Adaptive Suite 구성** 섹션에서 **Adaptive Suite 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-163">On the **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b6c66-164">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="b6c66-166">다른 웹 브라우저 창에서 Adaptive Suite 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-166">In a different web browser window, log in to your Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="b6c66-167">**관리자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-167">Go to **Admin**.</span></span>
   
    <span data-ttu-id="b6c66-168">![관리자](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="b6c66-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="b6c66-169">**사용자 및 역할** 섹션에서 **SAML SSO 설정 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-169">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="b6c66-170">![SAML SSO 설정 관리](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "SAML SSO 설정 관리")</span><span class="sxs-lookup"><span data-stu-id="b6c66-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="b6c66-171">**SAML SSO 설정** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-171">On the **SAML SSO Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="b6c66-172">![SAML SSO 설정](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO 설정")</span><span class="sxs-lookup"><span data-stu-id="b6c66-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="b6c66-173">a.</span><span class="sxs-lookup"><span data-stu-id="b6c66-173">a.</span></span> <span data-ttu-id="b6c66-174">**ID 공급자 이름** 텍스트 상자에 구성할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-174">In the **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="b6c66-175">b.</span><span class="sxs-lookup"><span data-stu-id="b6c66-175">b.</span></span> <span data-ttu-id="b6c66-176">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **ID 공급자 엔터티 ID** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-176">Paste the **SAML Entity ID** value copied from Azure portal into the **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="b6c66-177">c.</span><span class="sxs-lookup"><span data-stu-id="b6c66-177">c.</span></span> <span data-ttu-id="b6c66-178">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **ID 공급자 SSO URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-178">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="b6c66-179">d.</span><span class="sxs-lookup"><span data-stu-id="b6c66-179">d.</span></span> <span data-ttu-id="b6c66-180">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을  **사용자 지정 로그아웃 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-180">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="b6c66-181">e.</span><span class="sxs-lookup"><span data-stu-id="b6c66-181">e.</span></span> <span data-ttu-id="b6c66-182">다운로드한 인증서를 업로드하려면 **파일 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-182">To upload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="b6c66-183">f.</span><span class="sxs-lookup"><span data-stu-id="b6c66-183">f.</span></span> <span data-ttu-id="b6c66-184">다음과 같이 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-184">Select the following, for:</span></span>
    * <span data-ttu-id="b6c66-185">**SAML 사용자 ID**에 대해 **사용자의 Adaptive Insights 사용자 이름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="b6c66-186">**SAML 사용자 ID 위치**에 대해 **제목의 NameID에서 사용자 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="b6c66-187">**SAML NameID 형식**에 대해 **전자 메일 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="b6c66-188">**SAML 사용**에 대해 **SAML SSO 및 Adaptive Insights 직접 로그인 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="b6c66-189">g.</span><span class="sxs-lookup"><span data-stu-id="b6c66-189">g.</span></span> <span data-ttu-id="b6c66-190">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b6c66-191">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b6c66-192">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b6c66-193">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b6c66-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b6c66-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="b6c66-195">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b6c66-197">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="b6c66-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b6c66-198">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b6c66-200">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b6c66-202">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b6c66-204">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b6c66-206">a.</span><span class="sxs-lookup"><span data-stu-id="b6c66-206">a.</span></span> <span data-ttu-id="b6c66-207">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b6c66-208">b.</span><span class="sxs-lookup"><span data-stu-id="b6c66-208">b.</span></span> <span data-ttu-id="b6c66-209">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b6c66-210">c.</span><span class="sxs-lookup"><span data-stu-id="b6c66-210">c.</span></span> <span data-ttu-id="b6c66-211">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b6c66-212">d.</span><span class="sxs-lookup"><span data-stu-id="b6c66-212">d.</span></span> <span data-ttu-id="b6c66-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="b6c66-214">Adaptive Suite 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b6c66-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="b6c66-215">Azure AD 사용자가 Adaptive Suite에 로그인할 수 있도록 하려면 Adaptive Suite로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-215">To enable Azure AD users to log in to Adaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="b6c66-216">Adaptive Suite의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-216">In the case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="b6c66-217">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b6c66-217">**To configure user provisioning, perform the following steps:**</span></span> 

1. <span data-ttu-id="b6c66-218">**Adaptive Suite** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-218">Log in to your **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="b6c66-219">**관리자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-219">Go to **Admin**.</span></span>
   
   <span data-ttu-id="b6c66-220">![관리자](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="b6c66-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="b6c66-221">**사용자 및 역할** 섹션에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-221">In the **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="b6c66-222">![사용자 추가](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="b6c66-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="b6c66-223">**새 사용자** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-223">In the **New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="b6c66-224">![제출](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "제출")</span><span class="sxs-lookup"><span data-stu-id="b6c66-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="b6c66-225">a.</span><span class="sxs-lookup"><span data-stu-id="b6c66-225">a.</span></span> <span data-ttu-id="b6c66-226">관련된 텍스트 상자에 프로비전할 유효한 Azure Active Directory 사용자의 **이름**, **로그인**, **전자 메일**, **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-226">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span></span>
  
   <span data-ttu-id="b6c66-227">b.</span><span class="sxs-lookup"><span data-stu-id="b6c66-227">b.</span></span> <span data-ttu-id="b6c66-228">**역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="b6c66-229">c.</span><span class="sxs-lookup"><span data-stu-id="b6c66-229">c.</span></span> <span data-ttu-id="b6c66-230">**Submit**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="b6c66-231">다른 Adaptive Suite 사용자 계정 생성 도구 또는 Adaptive Suite가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b6c66-232">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="b6c66-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b6c66-233">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Adaptive Suite에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adaptive Suite.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b6c66-235">**Britta Simon을 Adaptive Suite에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b6c66-235">**To assign Britta Simon to Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="b6c66-236">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b6c66-238">응용 프로그램 목록에서 **Adaptive Suite**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-238">In the applications list, select **Adaptive Suite**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="b6c66-240">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-240">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b6c66-242">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-242">Click **Add** button.</span></span> <span data-ttu-id="b6c66-243">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b6c66-245">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b6c66-246">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b6c66-247">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b6c66-248">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b6c66-248">Testing single sign-on</span></span>

<span data-ttu-id="b6c66-249">이 섹션은 액세스 패널을 사용하여 Microsoft Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-249">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="b6c66-250">액세스 패널에서 Adaptive Suite 타일을 클릭하면 Adaptive Suite 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6c66-250">When you click the Adaptive Suite tile in the Access Panel, you should get automatically signed-on to your Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b6c66-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b6c66-251">Additional resources</span></span>

* [<span data-ttu-id="b6c66-252">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="b6c66-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b6c66-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b6c66-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png


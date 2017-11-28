---
title: "자습서: SpringCM과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 SpringCM 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: edfd06a06c730597fee4569ca1ce29092b45244a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="359b6-103">자습서: SpringCM과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="359b6-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="359b6-104">이 자습서에서는 Azure AD(Azure Active Directory)와 SpringCM을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-104">In this tutorial, you learn how to integrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="359b6-105">SpringCM과 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-105">Integrating SpringCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="359b6-106">SpringCM에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-106">You can control in Azure AD who has access to SpringCM</span></span>
- <span data-ttu-id="359b6-107">사용자가 해당 Azure AD 계정으로 SpringCM(Single Sign-on)에 자동으로 로그인하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-107">You can enable your users to automatically get signed-on to SpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="359b6-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="359b6-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="359b6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="359b6-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="359b6-110">Prerequisites</span></span>

<span data-ttu-id="359b6-111">SpringCM과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-111">To configure Azure AD integration with SpringCM, you need the following items:</span></span>

- <span data-ttu-id="359b6-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="359b6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="359b6-113">SpringCM Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="359b6-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="359b6-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="359b6-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="359b6-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="359b6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="359b6-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="359b6-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="359b6-118">Scenario description</span></span>
<span data-ttu-id="359b6-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="359b6-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="359b6-121">갤러리에서 SpringCM 추가</span><span class="sxs-lookup"><span data-stu-id="359b6-121">Adding SpringCM from the gallery</span></span>
2. <span data-ttu-id="359b6-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="359b6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-the-gallery"></a><span data-ttu-id="359b6-123">갤러리에서 SpringCM 추가</span><span class="sxs-lookup"><span data-stu-id="359b6-123">Adding SpringCM from the gallery</span></span>
<span data-ttu-id="359b6-124">SpringCM의 Azure AD 통합을 구성하려면 갤러리의 SpringCM을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-124">To configure the integration of SpringCM into Azure AD, you need to add SpringCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="359b6-125">**갤러리에서 SpringCM을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="359b6-125">**To add SpringCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="359b6-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="359b6-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="359b6-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="359b6-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="359b6-133">검색 상자에 **SpringCM**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-133">In the search box, type **SpringCM**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="359b6-135">결과 패널에서 **SpringCM**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-135">In the results panel, select **SpringCM**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="359b6-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="359b6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="359b6-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SpringCM에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="359b6-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 SpringCM 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SpringCM is to a user in Azure AD.</span></span> <span data-ttu-id="359b6-140">즉, Azure AD 사용자와 SpringCM의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-140">In other words, a link relationship between an Azure AD user and the related user in SpringCM needs to be established.</span></span>

<span data-ttu-id="359b6-141">SpringCM에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-141">In SpringCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="359b6-142">SpringCM에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-142">To configure and test Azure AD single sign-on with SpringCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="359b6-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="359b6-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="359b6-145">**[SpringCM 테스트 사용자 만들기](#creating-a-springcm-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 SpringCM에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - to have a counterpart of Britta Simon in SpringCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="359b6-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="359b6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="359b6-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="359b6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="359b6-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 SpringCM 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="359b6-150">**SpringCM에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="359b6-150">**To configure Azure AD single sign-on with SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="359b6-151">Azure Portal의 **SpringCM** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-151">In the Azure portal, on the **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="359b6-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="359b6-155">**SpringCM 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-155">On the **SpringCM Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="359b6-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="359b6-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="359b6-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-158">This value is not real.</span></span> <span data-ttu-id="359b6-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="359b6-160">이 값을 얻으려면 [SpringCM 클라이언트 지원 팀](https://knowledge.springcm.com/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="359b6-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) to get this value.</span></span> 
 
4. <span data-ttu-id="359b6-161">**SAML 서명 인증서** 섹션에서 **인증서(원시)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="359b6-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="359b6-165">**SpringCM 구성** 섹션에서 **SpringCM 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-165">On the **SpringCM Configuration** section, click **Configure SpringCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="359b6-166">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="359b6-168">다른 웹 브라우저 창에서 **SpringCM** 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-168">In a different web browser window, sign on to your **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="359b6-169">위쪽에 있는 메뉴에서 **이동**을 클릭하고 **기본 설정**을 클릭한 다음 **계정 기본 설정** 섹션에서 **SAML SSO**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-169">In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="359b6-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span><span class="sxs-lookup"><span data-stu-id="359b6-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="359b6-171">ID 공급자 구성 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-171">In the Identity Provider Configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="359b6-172">![ID 공급자 구성](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "ID 공급자 구성")</span><span class="sxs-lookup"><span data-stu-id="359b6-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="359b6-173">a.</span><span class="sxs-lookup"><span data-stu-id="359b6-173">a.</span></span> <span data-ttu-id="359b6-174">다운로드한 Azure Active Directory 인증서를 업로드하려면 **발급자 인증서 선택** 또는 **발급자 인증서 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-174">To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="359b6-175">b.</span><span class="sxs-lookup"><span data-stu-id="359b6-175">b.</span></span> <span data-ttu-id="359b6-176">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into the **Issuer** textbox.</span></span>
    
    <span data-ttu-id="359b6-177">c.</span><span class="sxs-lookup"><span data-stu-id="359b6-177">c.</span></span> <span data-ttu-id="359b6-178">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **SP(서비스 공급자)가 시작한 끝점** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="359b6-179">d.</span><span class="sxs-lookup"><span data-stu-id="359b6-179">d.</span></span> <span data-ttu-id="359b6-180">**사용**으로 **SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="359b6-181">e.</span><span class="sxs-lookup"><span data-stu-id="359b6-181">e.</span></span> <span data-ttu-id="359b6-182">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="359b6-183">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="359b6-184">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="359b6-185">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="359b6-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="359b6-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="359b6-187">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="359b6-189">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="359b6-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="359b6-190">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="359b6-192">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="359b6-194">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="359b6-196">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="359b6-198">a.</span><span class="sxs-lookup"><span data-stu-id="359b6-198">a.</span></span> <span data-ttu-id="359b6-199">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="359b6-200">b.</span><span class="sxs-lookup"><span data-stu-id="359b6-200">b.</span></span> <span data-ttu-id="359b6-201">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="359b6-202">c.</span><span class="sxs-lookup"><span data-stu-id="359b6-202">c.</span></span> <span data-ttu-id="359b6-203">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="359b6-204">d.</span><span class="sxs-lookup"><span data-stu-id="359b6-204">d.</span></span> <span data-ttu-id="359b6-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="359b6-206">SpringCM 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="359b6-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="359b6-207">Azure Active Directory 사용자가 SpringCM에 로그인할 수 있도록 하려면 SpringCM으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-207">To enable Azure Active Directory users to log in to SpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="359b6-208">SpringCM의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-208">In the case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="359b6-209">자세한 내용은 [SpringCM 사용자 만들기 및 편집](http://knowledge.springcm.com/create-and-edit-a-springcm-user)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="359b6-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="359b6-210">**사용자 계정을 SpringCM에 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="359b6-210">**To provision a user account to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="359b6-211">**SpringCM** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-211">Log in to your **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="359b6-212">**GOTO**를 클릭하고 **주소록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="359b6-213">![사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="359b6-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="359b6-214">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-214">Click **Create User**.</span></span>

4. <span data-ttu-id="359b6-215">**사용자 역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="359b6-216">**활성화 메일 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="359b6-217">관련된 텍스트 상자에 프로비전할 유효한 Azure Active Directory 사용자 계정의 이름, 성 및 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-217">Type the first name, last name, and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.</span></span>

7. <span data-ttu-id="359b6-218">**보안 그룹**에 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-218">Add the user to a **Security group**.</span></span>

8. <span data-ttu-id="359b6-219">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="359b6-220">다른 SpringCM 사용자 계정 생성 도구 또는 SpringCM이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.</span></span>  
  > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="359b6-221">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="359b6-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="359b6-222">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 SpringCM에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SpringCM.</span></span>

![사용자 할당][200] 

<span data-ttu-id="359b6-224">**Britta Simon을 SpringCM에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="359b6-224">**To assign Britta Simon to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="359b6-225">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="359b6-227">응용 프로그램 목록에서 **SpringCM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-227">In the applications list, select **SpringCM**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="359b6-229">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-229">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="359b6-231">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-231">Click **Add** button.</span></span> <span data-ttu-id="359b6-232">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="359b6-234">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="359b6-235">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="359b6-236">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="359b6-237">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="359b6-237">Testing single sign-on</span></span>

<span data-ttu-id="359b6-238">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="359b6-239">액세스 패널에서 SpringCM 타일을 클릭하면 SpringCM 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="359b6-239">When you click the SpringCM tile in the Access Panel, you should get automatically signed-on to your SpringCM application.</span></span>

<span data-ttu-id="359b6-240">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="359b6-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="359b6-241">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="359b6-241">Additional resources</span></span>

* [<span data-ttu-id="359b6-242">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="359b6-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="359b6-243">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="359b6-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png


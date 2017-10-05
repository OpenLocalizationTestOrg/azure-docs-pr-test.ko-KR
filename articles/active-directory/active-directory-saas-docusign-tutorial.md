---
title: "자습서: DocuSign과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 DocuSign 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 29c99fdf39d366df90abc070f7b836320935035c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="5bc20-103">자습서: DocuSign와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5bc20-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="5bc20-104">이 자습서에서는 Azure AD(Azure Active Directory)와 DocuSign을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-104">In this tutorial, you learn how to integrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bc20-105">DocuSign을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-105">Integrating DocuSign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5bc20-106">DocuSign에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-106">You can control in Azure AD who has access to DocuSign</span></span>
- <span data-ttu-id="5bc20-107">사용자가 해당 Azure AD 계정으로 DocuSign에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-107">You can enable your users to automatically get signed-on to DocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bc20-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5bc20-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5bc20-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bc20-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5bc20-110">Prerequisites</span></span>

<span data-ttu-id="5bc20-111">DocuSign과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-111">To configure Azure AD integration with DocuSign, you need the following items:</span></span>

- <span data-ttu-id="5bc20-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5bc20-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bc20-113">DocuSign Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5bc20-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bc20-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bc20-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bc20-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5bc20-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bc20-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bc20-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5bc20-118">Scenario description</span></span>
<span data-ttu-id="5bc20-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bc20-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bc20-121">갤러리에서 DocuSign 추가</span><span class="sxs-lookup"><span data-stu-id="5bc20-121">Adding DocuSign from the gallery</span></span>
2. <span data-ttu-id="5bc20-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5bc20-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-the-gallery"></a><span data-ttu-id="5bc20-123">갤러리에서 DocuSign 추가</span><span class="sxs-lookup"><span data-stu-id="5bc20-123">Adding DocuSign from the gallery</span></span>
<span data-ttu-id="5bc20-124">DocuSign의 Azure AD 통합을 구성하려면 갤러리의 DocuSign을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-124">To configure the integration of DocuSign into Azure AD, you need to add DocuSign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5bc20-125">**갤러리에서 DocuSign을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5bc20-125">**To add DocuSign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5bc20-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5bc20-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5bc20-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5bc20-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-131">Click **New application** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5bc20-133">검색 상자에 **DocuSign**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-133">In the search box, type **DocuSign**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="5bc20-135">결과 패널에서 **DocuSign**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-135">In the results panel, select **DocuSign**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5bc20-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5bc20-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5bc20-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 DocuSign에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5bc20-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 DocuSign 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DocuSign is to a user in Azure AD.</span></span> <span data-ttu-id="5bc20-140">즉, Azure AD 사용자와 DocuSign의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-140">In other words, a link relationship between an Azure AD user and the related user in DocuSign needs to be established.</span></span>

<span data-ttu-id="5bc20-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 DocuSign의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in DocuSign.</span></span>

<span data-ttu-id="5bc20-142">DocuSign에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-142">To configure and test Azure AD single sign-on with DocuSign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5bc20-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5bc20-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bc20-145">**[DocuSign 테스트 사용자 만들기](#creating-a-docusign-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 DocuSign에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - to have a counterpart of Britta Simon in DocuSign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bc20-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bc20-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5bc20-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5bc20-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5bc20-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 DocuSign 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="5bc20-150">**DocuSign에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5bc20-150">**To configure Azure AD single sign-on with DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="5bc20-151">Azure Portal의 **DocuSign** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-151">In the Azure portal, on the **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5bc20-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="5bc20-155">**SAML 서명 인증서** 섹션에서 **인증서(Base 64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-155">On the **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="5bc20-157">Azure Portal의 **DocuSign 구성** 섹션에서 **DocuSign 구성**을 클릭하여 로그온 구성 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-157">On the **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** to open Configure sign-on window.</span></span> <span data-ttu-id="5bc20-158">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-158">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="5bc20-160">다른 웹 브라우저 창에서 **DocuSign 관리 포털**에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-160">In a different web browser window, login to your **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="5bc20-161">왼쪽 탐색 메뉴에서 **도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-161">In the navigation menu on the left, click **Domains**.</span></span>
   
    ![Single Sign-On 구성][51]

7. <span data-ttu-id="5bc20-163">오른쪽 창에서 **도메인 클레임**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-163">On the right pane, click **Claim Domain**.</span></span>
   
    ![Single Sign-On 구성][52]

8. <span data-ttu-id="5bc20-165">**도메인 클레임** 대화 상자의 **도메인 이름** 텍스트 상자에 회사 도메인을 입력한 다음 **클레임**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-165">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="5bc20-166">도메인을 확인하고 상태가 활성인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-166">Make sure that you verify the domain and the status is active.</span></span>
   
    ![Single Sign-On 구성][53]

9. <span data-ttu-id="5bc20-168">왼쪽 메뉴에서 **ID 공급자**</span><span class="sxs-lookup"><span data-stu-id="5bc20-168">In menu on the left side, click **Identity Providers**</span></span>  
   
    ![Single Sign-On 구성][54]
10. <span data-ttu-id="5bc20-170">오른쪽 창에서 **ID 공급자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-170">In the right pane, click **Add Identity Provider**.</span></span> 
   
    ![Single Sign-On 구성][55]

11. <span data-ttu-id="5bc20-172">**ID 공급자 설정** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-172">On the **Identity Provider Settings** page, perform the following steps:</span></span>
   
    ![Single Sign-On 구성][56]

    <span data-ttu-id="5bc20-174">a.</span><span class="sxs-lookup"><span data-stu-id="5bc20-174">a.</span></span> <span data-ttu-id="5bc20-175">**이름** 텍스트 상자에 구성할 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-175">In the **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="5bc20-176">공백을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5bc20-176">Do not use spaces.</span></span>

    <span data-ttu-id="5bc20-177">b.</span><span class="sxs-lookup"><span data-stu-id="5bc20-177">b.</span></span> <span data-ttu-id="5bc20-178">**SAML 엔터티 ID**를 **ID 공급자 발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-178">Paste **SAML Entity ID** into the **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="5bc20-179">c.</span><span class="sxs-lookup"><span data-stu-id="5bc20-179">c.</span></span> <span data-ttu-id="5bc20-180">**SAML Single Sign-On 서비스 URL**을 **ID 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-180">Paste **SAML Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="5bc20-181">d.</span><span class="sxs-lookup"><span data-stu-id="5bc20-181">d.</span></span> <span data-ttu-id="5bc20-182">**로그아웃 URL**을 **ID 공급자 로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-182">Paste **Sign-Out URL** into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="5bc20-183">e.</span><span class="sxs-lookup"><span data-stu-id="5bc20-183">e.</span></span> <span data-ttu-id="5bc20-184">**Sign AuthN 요청**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="5bc20-185">f.</span><span class="sxs-lookup"><span data-stu-id="5bc20-185">f.</span></span> <span data-ttu-id="5bc20-186">**AuthN 요청 보내기**로 **POST**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="5bc20-187">g.</span><span class="sxs-lookup"><span data-stu-id="5bc20-187">g.</span></span> <span data-ttu-id="5bc20-188">**로그아웃 요청 보내기**로 **GET**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="5bc20-189">**사용자 지정 특성 매핑** 섹션에서 Azure AD 클레임을 사용하여 매핑하려는 필드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-189">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span></span> <span data-ttu-id="5bc20-190">이 예제에서는 **emailaddress** 클레임이 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress** 값으로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-190">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="5bc20-191">이는 Azure AD의 메일 클레임에 대한 기본 클레임 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-191">It is the default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="5bc20-192">적절한 **사용자 ID**를 사용하여 Azure AD에서 DocuSign 사용자 매핑으로 사용자를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-192">Use the appropriate **User identifier** to map the user from Azure AD to DocuSign user mapping.</span></span> <span data-ttu-id="5bc20-193">적절한 필드를 선택하고 조직 설정에 따라 적절한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-193">Select the proper Field and enter the appropriate value based on your organization settings.</span></span>
          
    ![Single Sign-On 구성][57]

13. <span data-ttu-id="5bc20-195">**ID 공급자 인증서** 섹션에서 **인증서 추가**를 클릭하고 Azure AD 포털에서 다운로드한 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-195">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Single Sign-On 구성][58]

14. <span data-ttu-id="5bc20-197">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-197">Click **Save**.</span></span>

15. <span data-ttu-id="5bc20-198">**ID 공급자** 섹션에서 **작업**을 클릭한 다음 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-198">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Single Sign-On 구성][59]
 
16. <span data-ttu-id="5bc20-200">**DocuSign 관리자 포털**의 **SAML 2.0 끝점 보기** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-200">In the **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform the following steps:</span></span>
   
    ![Single Sign-On 구성][60]
   
    <span data-ttu-id="5bc20-202">a.</span><span class="sxs-lookup"><span data-stu-id="5bc20-202">a.</span></span> <span data-ttu-id="5bc20-203">**서비스 공급자 발급자 URL**을 복사하여 Azure Portal **DocuSign 도메인 및 URL** 섹션의 **식별자** 텍스트 상자에 `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>` 패턴에 따라 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-203">Copy the **Service Provider Issuer URL**, and then paste into the **Identifier** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="5bc20-204">b.</span><span class="sxs-lookup"><span data-stu-id="5bc20-204">b.</span></span> <span data-ttu-id="5bc20-205">**서비스 공급자 로그인 URL**을 복사하여 Azure Portal **DocuSign 도메인 및 URL** 섹션의 **로그온 URL** 텍스트 상자에 `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`패턴에 따라 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-205">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="5bc20-207">c.</span><span class="sxs-lookup"><span data-stu-id="5bc20-207">c.</span></span>  <span data-ttu-id="5bc20-208">페이지 맨 아래에 있는 **닫기**</span><span class="sxs-lookup"><span data-stu-id="5bc20-208">Click **Close**</span></span>
    
17. <span data-ttu-id="5bc20-209">Azure Portal에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-209">On the Azure portal, click **Save**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="5bc20-211">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5bc20-212">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5bc20-213">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5bc20-214">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5bc20-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="5bc20-215">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5bc20-217">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="5bc20-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5bc20-218">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bc20-220">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bc20-222">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bc20-224">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bc20-226">a.</span><span class="sxs-lookup"><span data-stu-id="5bc20-226">a.</span></span> <span data-ttu-id="5bc20-227">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bc20-228">b.</span><span class="sxs-lookup"><span data-stu-id="5bc20-228">b.</span></span> <span data-ttu-id="5bc20-229">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bc20-230">c.</span><span class="sxs-lookup"><span data-stu-id="5bc20-230">c.</span></span> <span data-ttu-id="5bc20-231">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5bc20-232">d.</span><span class="sxs-lookup"><span data-stu-id="5bc20-232">d.</span></span> <span data-ttu-id="5bc20-233">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="5bc20-234">DocuSign 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5bc20-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="5bc20-235">응용 프로그램이 **Just-In-Time 사용자 프로비전**을 지원하며 인증 후에는 응용 프로그램에서 자동으로 사용자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-235">Application supports **Just in time user provisioning** and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5bc20-236">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="5bc20-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5bc20-237">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 DocuSign에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-237">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to DocuSign.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5bc20-239">**Britta Simon을 DocuSign에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="5bc20-239">**To assign Britta Simon to DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="5bc20-240">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5bc20-242">응용 프로그램 목록에서 **DocuSign**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-242">In the applications list, select **DocuSign**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="5bc20-244">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-244">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5bc20-246">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-246">Click **Add** button.</span></span> <span data-ttu-id="5bc20-247">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5bc20-249">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5bc20-250">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bc20-251">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5bc20-252">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5bc20-252">Testing single sign-on</span></span>

<span data-ttu-id="5bc20-253">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5bc20-254">액세스 패널에서 DocuSign 타일을 클릭하면 DocuSign 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bc20-254">When you click the DocuSign tile in the Access Panel, you should get automatically signed-on to your DocuSign application.</span></span>
<span data-ttu-id="5bc20-255">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5bc20-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5bc20-256">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5bc20-256">Additional resources</span></span>

* [<span data-ttu-id="5bc20-257">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="5bc20-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bc20-258">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5bc20-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="5bc20-259">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="5bc20-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png


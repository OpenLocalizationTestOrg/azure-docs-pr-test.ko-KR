---
title: "자습서: Boomi와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Boomi 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 1121d22beddf73fd2109a4b410422f76dd37478e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="ea756-103">자습서: Boomi와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="ea756-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="ea756-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Boomi를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea756-105">Boomi를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-105">Integrating Boomi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ea756-106">Boomi에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-106">You can control in Azure AD who has access to Boomi</span></span>
- <span data-ttu-id="ea756-107">사용자가 해당 Azure AD 계정으로 Boomi에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea756-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ea756-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea756-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea756-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ea756-110">Prerequisites</span></span>

<span data-ttu-id="ea756-111">Boomi와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-111">To configure Azure AD integration with Boomi, you need the following items:</span></span>

- <span data-ttu-id="ea756-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="ea756-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea756-113">Boomi Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="ea756-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea756-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea756-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea756-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ea756-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea756-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea756-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="ea756-118">Scenario description</span></span>
<span data-ttu-id="ea756-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea756-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea756-121">갤러리에서 Boomi 추가</span><span class="sxs-lookup"><span data-stu-id="ea756-121">Adding Boomi from the gallery</span></span>
2. <span data-ttu-id="ea756-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ea756-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-the-gallery"></a><span data-ttu-id="ea756-123">갤러리에서 Boomi 추가</span><span class="sxs-lookup"><span data-stu-id="ea756-123">Adding Boomi from the gallery</span></span>
<span data-ttu-id="ea756-124">Boomi의 Azure AD 통합을 구성하려면 갤러리의 Boomi를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ea756-125">**갤러리에서 Boomi를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ea756-125">**To add Boomi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ea756-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ea756-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ea756-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="ea756-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="ea756-133">검색 상자에 **Boomi**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-133">In the search box, type **Boomi**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="ea756-135">결과 창에서 **Boomi**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-135">In the results panel, select **Boomi**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea756-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ea756-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea756-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Boomi에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ea756-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Boomi 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span></span> <span data-ttu-id="ea756-140">즉, Azure AD 사용자와 Boomi의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-140">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span></span>

<span data-ttu-id="ea756-141">Boomi에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-141">In Boomi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ea756-142">Boomi에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-142">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ea756-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ea756-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea756-145">**[Boomi 테스트 사용자 만들기](#creating-a-boomi-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Boomi에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea756-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea756-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea756-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="ea756-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea756-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Boomi 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="ea756-150">**Boomi에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ea756-150">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="ea756-151">Azure Portal의 **Boomi** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-151">In the Azure portal, on the **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="ea756-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="ea756-155">**Boomi 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-155">On the **Boomi Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="ea756-157">a.</span><span class="sxs-lookup"><span data-stu-id="ea756-157">a.</span></span> <span data-ttu-id="ea756-158">**식별자** 텍스트 상자에서 `https://platform.boomi.com/sso/<accountname>/saml` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-158">In the **Identifier** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="ea756-159">b.</span><span class="sxs-lookup"><span data-stu-id="ea756-159">b.</span></span> <span data-ttu-id="ea756-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="ea756-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea756-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-161">These values are not real.</span></span> <span data-ttu-id="ea756-162">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="ea756-163">이러한 값을 얻으려면 [Boomi 지원 팀](https://boomi.com/company/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="ea756-163">Contact [Boomi support team](https://boomi.com/company/contact/) to get these values.</span></span>

4. <span data-ttu-id="ea756-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="ea756-166">Boomi 응용 프로그램에는 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-166">Boomi application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ea756-167">이 응용 프로그램에 대한 다음 클레임을 구성하세요.</span><span class="sxs-lookup"><span data-stu-id="ea756-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="ea756-168">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-168">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ea756-169">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-169">The following screenshot shows an example for this.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="ea756-171">**Single sign on** 대화 상자의 **사용자 특성** 섹션에서 아래 표에 표시되는 각 행에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-171">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span></span>

    | <span data-ttu-id="ea756-172">특성 이름</span><span class="sxs-lookup"><span data-stu-id="ea756-172">Attribute Name</span></span> | <span data-ttu-id="ea756-173">특성 값</span><span class="sxs-lookup"><span data-stu-id="ea756-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="ea756-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="ea756-174">FEDERATION_ID</span></span> | <span data-ttu-id="ea756-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="ea756-175">user.mail</span></span> |
    
    <span data-ttu-id="ea756-176">a.</span><span class="sxs-lookup"><span data-stu-id="ea756-176">a.</span></span> <span data-ttu-id="ea756-177">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Single Sign-On 구성](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Single Sign-on 구성](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ea756-180">b.</span><span class="sxs-lookup"><span data-stu-id="ea756-180">b.</span></span> <span data-ttu-id="ea756-181">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ea756-182">c.</span><span class="sxs-lookup"><span data-stu-id="ea756-182">c.</span></span> <span data-ttu-id="ea756-183">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ea756-184">d.</span><span class="sxs-lookup"><span data-stu-id="ea756-184">d.</span></span> <span data-ttu-id="ea756-185">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-185">Click **Ok**.</span></span>

6. <span data-ttu-id="ea756-186">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-186">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ea756-188">**Boomi 구성** 섹션에서 **Boomi 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-188">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ea756-189">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-189">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="ea756-191">다른 웹 브라우저 창에서 Boomi 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="ea756-192">**회사 이름**, **설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-192">Navigate to **Company Name** and go to **Set up**.</span></span>

10. <span data-ttu-id="ea756-193">**SSO 옵션** 탭을 클릭하고 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-193">Click the **SSO Options** tab and perform below steps.</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="ea756-195">a.</span><span class="sxs-lookup"><span data-stu-id="ea756-195">a.</span></span> <span data-ttu-id="ea756-196">**SAML Single Sign-On 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="ea756-197">b.</span><span class="sxs-lookup"><span data-stu-id="ea756-197">b.</span></span> <span data-ttu-id="ea756-198">**가져오기**를 클릭하여 Azure AD에서 다운로드한 인증서를 **ID 공급자 인증서**로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-198">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="ea756-199">c.</span><span class="sxs-lookup"><span data-stu-id="ea756-199">c.</span></span> <span data-ttu-id="ea756-200">**ID 공급자 로그인 URL** 텍스트 상자에 Azure AD 응용 프로그램 구성 창의 **SAML Single Sign-On 서비스 URL** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-200">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="ea756-201">d.</span><span class="sxs-lookup"><span data-stu-id="ea756-201">d.</span></span> <span data-ttu-id="ea756-202">**페더레이션 ID 위치**로 **페더레이션 ID는 FEDERATION_ID 특성 요소입니다** 라디오 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="ea756-203">e.</span><span class="sxs-lookup"><span data-stu-id="ea756-203">e.</span></span> <span data-ttu-id="ea756-204">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="ea756-205">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ea756-206">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ea756-207">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea756-208">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ea756-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea756-209">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="ea756-211">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="ea756-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ea756-212">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea756-214">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea756-216">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea756-218">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea756-220">a.</span><span class="sxs-lookup"><span data-stu-id="ea756-220">a.</span></span> <span data-ttu-id="ea756-221">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea756-222">b.</span><span class="sxs-lookup"><span data-stu-id="ea756-222">b.</span></span> <span data-ttu-id="ea756-223">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea756-224">c.</span><span class="sxs-lookup"><span data-stu-id="ea756-224">c.</span></span> <span data-ttu-id="ea756-225">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ea756-226">d.</span><span class="sxs-lookup"><span data-stu-id="ea756-226">d.</span></span> <span data-ttu-id="ea756-227">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="ea756-228">Boomi 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ea756-228">Creating a Boomi test user</span></span>

<span data-ttu-id="ea756-229">Azure AD 사용자가 Boomi에 로그인할 수 있도록 하려면 Boomi로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-229">In order to enable Azure AD users to log in to Boomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="ea756-230">Boomi의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-230">In the case of Boomi, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="ea756-231">사용자 계정을 프로비저닝하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-231">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="ea756-232">Boomi 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-232">Log in to your Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="ea756-233">로그인 후 **사용자 관리**, **사용자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-233">After logging in, navigate to **User Management** and go to **Users**.</span></span>

    <span data-ttu-id="ea756-234">![사용자](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="ea756-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="ea756-235"> **+**  아이콘을 클릭하면 **사용자 역할 추가/유지 관리** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-235">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="ea756-236">![사용자](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="ea756-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="ea756-237">![사용자](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="ea756-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="ea756-238">a.</span><span class="sxs-lookup"><span data-stu-id="ea756-238">a.</span></span> <span data-ttu-id="ea756-239">**사용자 메일 주소** 텍스트 상자에서 BrittaSimon@contoso.com과 같은 사용자의 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-239">In the **User e-mail address** textbox, type the email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="ea756-240">b.</span><span class="sxs-lookup"><span data-stu-id="ea756-240">b.</span></span> <span data-ttu-id="ea756-241">**이름** 텍스트 상자에 사용자의 이름(예: Britta)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-241">In the **First name** textbox, type the First name of user like Britta.</span></span>

    <span data-ttu-id="ea756-242">c.</span><span class="sxs-lookup"><span data-stu-id="ea756-242">c.</span></span> <span data-ttu-id="ea756-243">**성** 텍스트 상자에 사용자의 성(예: Simon)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-243">In the **Last name** textbox, type the Last name of user like Simon.</span></span>
    
    <span data-ttu-id="ea756-244">d.</span><span class="sxs-lookup"><span data-stu-id="ea756-244">d.</span></span> <span data-ttu-id="ea756-245">사용자의 **페더레이션 ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-245">Enter the user's **Federation ID**.</span></span> <span data-ttu-id="ea756-246">각 사용자는 계정 내에서 사용자를 고유하게 식별하는 페더레이션 ID가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-246">Each user must have a Federation ID that uniquely identifies the user within the account.</span></span>
    
    <span data-ttu-id="ea756-247">e.</span><span class="sxs-lookup"><span data-stu-id="ea756-247">e.</span></span> <span data-ttu-id="ea756-248">**표준 사용자** 역할을 사용자에게 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-248">Assign the **Standard User** role to the user.</span></span> <span data-ttu-id="ea756-249">관리자 역할은 일반적인AtomSphere 액세스 권한과 Single Sign-On 액세스 권한을 모두 제공하므로 이 역할을 할당하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ea756-249">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="ea756-250">f.</span><span class="sxs-lookup"><span data-stu-id="ea756-250">f.</span></span> <span data-ttu-id="ea756-251">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ea756-252">사용자는 해당 암호가 ID 공급자를 통해 관리되므로 AtomSphere 계정에 로그인하는 데 사용할 수 있는 암호가 포함된 시작 알림 메일이 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-252">The user will not receive a welcome notification email containing a password that can be used to log in to the AtomSphere account because his password is managed through the identity provider.</span></span> <span data-ttu-id="ea756-253">다른 Boomi 사용자 계정 생성 도구 또는 Boomi가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-253">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ea756-254">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="ea756-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ea756-255">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Boomi에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boomi.</span></span>

![사용자 할당][200] 

<span data-ttu-id="ea756-257">**Britta Simon을 Boomi에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="ea756-257">**To assign Britta Simon to Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="ea756-258">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="ea756-260">응용 프로그램 목록에서 **Boomi**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-260">In the applications list, select **Boomi**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="ea756-262">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-262">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="ea756-264">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-264">Click **Add** button.</span></span> <span data-ttu-id="ea756-265">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="ea756-267">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ea756-268">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea756-269">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea756-270">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="ea756-270">Testing single sign-on</span></span>

<span data-ttu-id="ea756-271">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-271">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ea756-272">액세스 패널에서 Boomi 타일을 클릭하면 Boomi 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea756-272">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea756-273">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ea756-273">Additional resources</span></span>

* [<span data-ttu-id="ea756-274">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="ea756-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea756-275">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ea756-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png


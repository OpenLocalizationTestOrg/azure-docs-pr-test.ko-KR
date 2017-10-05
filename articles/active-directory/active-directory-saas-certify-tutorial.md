---
title: "자습서: Certify와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Certify 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bbb2357d17535de438555a0b1f8256b134c8a40e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="68298-103">자습서: Certify와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="68298-103">Tutorial: Azure Active Directory integration with Certify</span></span>

<span data-ttu-id="68298-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Certify를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="68298-104">In this tutorial, you learn how to integrate Certify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68298-105">Certify를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="68298-105">Integrating Certify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="68298-106">Certify에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68298-106">You can control in Azure AD who has access to Certify</span></span>
- <span data-ttu-id="68298-107">사용자가 해당 Azure AD 계정으로 Certify에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68298-107">You can enable your users to automatically get signed-on to Certify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68298-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68298-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="68298-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68298-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68298-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="68298-110">Prerequisites</span></span>

<span data-ttu-id="68298-111">Certify와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-111">To configure Azure AD integration with Certify, you need the following items:</span></span>

- <span data-ttu-id="68298-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="68298-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68298-113">Certify Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="68298-113">A Certify single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68298-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68298-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68298-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68298-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="68298-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68298-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68298-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68298-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="68298-118">Scenario description</span></span>
<span data-ttu-id="68298-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68298-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68298-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68298-121">갤러리에서 Certify 추가</span><span class="sxs-lookup"><span data-stu-id="68298-121">Adding Certify from the gallery</span></span>
2. <span data-ttu-id="68298-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="68298-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certify-from-the-gallery"></a><span data-ttu-id="68298-123">갤러리에서 Certify 추가</span><span class="sxs-lookup"><span data-stu-id="68298-123">Adding Certify from the gallery</span></span>
<span data-ttu-id="68298-124">Certify와 Azure AD의 통합을 구성하려면 갤러리의 Certify를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-124">To configure the integration of Certify into Azure AD, you need to add Certify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="68298-125">**갤러리에서 Certify를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="68298-125">**To add Certify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="68298-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="68298-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="68298-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="68298-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="68298-133">검색 상자에 **Certify**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-133">In the search box, type **Certify**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-certify-tutorial/tutorial_certify_search.png)

5. <span data-ttu-id="68298-135">결과 패널에서 **Certify**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-135">In the results panel, select **Certify**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-certify-tutorial/tutorial_certify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="68298-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="68298-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="68298-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Certify에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="68298-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Certify 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Certify is to a user in Azure AD.</span></span> <span data-ttu-id="68298-140">즉, Azure AD 사용자와 Certify의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-140">In other words, a link relationship between an Azure AD user and the related user in Certify needs to be established.</span></span>

<span data-ttu-id="68298-141">Certify에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-141">In Certify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="68298-142">Certify에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-142">To configure and test Azure AD single sign-on with Certify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="68298-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="68298-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68298-145">**[Certify 테스트 사용자 만들기](#creating-a-certify-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Certify에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68298-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="68298-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68298-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="68298-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="68298-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="68298-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Certify 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Certify application.</span></span>

<span data-ttu-id="68298-150">**Certify에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="68298-150">**To configure Azure AD single sign-on with Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="68298-151">Azure Portal의 **Certify** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-151">In the Azure portal, on the **Certify** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="68298-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-certify-tutorial/tutorial_certify_samlbase.png)

3. <span data-ttu-id="68298-155">**Certify 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-155">On the **Certify Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-certify-tutorial/tutorial_certify_url.png)

    <span data-ttu-id="68298-157">**식별자** 텍스트 상자에 URL `https://www.certify.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-157">In the **Identifier** textbox, type the URL: `https://www.certify.com`</span></span>

4. <span data-ttu-id="68298-158">**SAML 서명 인증서** 섹션에서 **인증서(원시)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-158">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-certify-tutorial/tutorial_certify_certificate.png) 

5. <span data-ttu-id="68298-160">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-160">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-certify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="68298-162">**Certify 구성** 섹션에서 **Certify 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68298-162">On the **Certify Configuration** section, click **Configure Certify** to open **Configure sign-on** window.</span></span> <span data-ttu-id="68298-163">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-certify-tutorial/tutorial_certify_configure.png) 

7. <span data-ttu-id="68298-165">**Certify** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **인증서(원시)**, **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 [Certify 지원 팀](mailto:support@certify.com)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-165">To configure single sign-on on **Certify** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Certify support team](mailto:support@certify.com).</span></span> <span data-ttu-id="68298-166">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="68298-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="68298-167">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68298-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="68298-168">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68298-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="68298-169">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68298-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="68298-170">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="68298-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="68298-171">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68298-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="68298-173">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="68298-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="68298-174">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-certify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68298-176">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-certify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68298-178">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-certify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68298-180">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-certify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68298-182">a.</span><span class="sxs-lookup"><span data-stu-id="68298-182">a.</span></span> <span data-ttu-id="68298-183">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68298-184">b.</span><span class="sxs-lookup"><span data-stu-id="68298-184">b.</span></span> <span data-ttu-id="68298-185">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68298-186">c.</span><span class="sxs-lookup"><span data-stu-id="68298-186">c.</span></span> <span data-ttu-id="68298-187">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="68298-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="68298-188">d.</span><span class="sxs-lookup"><span data-stu-id="68298-188">d.</span></span> <span data-ttu-id="68298-189">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-189">Click **Create**.</span></span>
 
### <a name="creating-a-certify-test-user"></a><span data-ttu-id="68298-190">Certify 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="68298-190">Creating a Certify test user</span></span>

<span data-ttu-id="68298-191">이 섹션은 Certify에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68298-191">The objective of this section is to create a user called Britta Simon in Certify.</span></span> <span data-ttu-id="68298-192">Certify는 적시 프로비전을 지원하며 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="68298-192">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="68298-193">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68298-193">There is no action item for you in this section.</span></span> <span data-ttu-id="68298-194">아직 새 사용자가 없으면 Certify에 액세스하는 동안 생성될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68298-194">A new user will be created during an attempt to access Certify if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="68298-195">사용자를 수동으로 생성해야 하는 경우 [Certify 지원 팀](mailto:support@certify.com)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-195">If you need to create an user manually, you need to contact the [Certify support team](mailto:support@certify.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="68298-196">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="68298-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="68298-197">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Certify에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Certify.</span></span>

![사용자 할당][200] 

<span data-ttu-id="68298-199">**Britta Simon을 Certify에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="68298-199">**To assign Britta Simon to Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="68298-200">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="68298-202">응용 프로그램 목록에서 **Certify**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-202">In the applications list, select **Certify**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-certify-tutorial/tutorial_certify_app.png) 

3. <span data-ttu-id="68298-204">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-204">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="68298-206">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-206">Click **Add** button.</span></span> <span data-ttu-id="68298-207">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="68298-209">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="68298-210">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68298-211">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68298-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="68298-212">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="68298-212">Testing single sign-on</span></span>

<span data-ttu-id="68298-213">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68298-213">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="68298-214">액세스 패널에서 Certify 타일을 클릭하면 Certify 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="68298-214">When you click the Certify tile in the Access Panel, you should get automatically signed-on to your Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68298-215">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="68298-215">Additional resources</span></span>

* [<span data-ttu-id="68298-216">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="68298-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68298-217">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="68298-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-certify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-certify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-certify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-certify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-certify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-certify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-certify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-certify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-certify-tutorial/tutorial_general_203.png


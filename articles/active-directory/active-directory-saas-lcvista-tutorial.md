---
title: "자습서: LCVista와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 LCVista 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c19f81da495eb7116b62797d1755d312a23f3805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="1724a-103">자습서: LCVista와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1724a-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="1724a-104">이 자습서에서는 Azure AD(Azure Active Directory)와 LCVista를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-104">In this tutorial, you learn how to integrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1724a-105">LCVista를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-105">Integrating LCVista with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1724a-106">LCVista에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-106">You can control in Azure AD who has access to LCVista</span></span>
- <span data-ttu-id="1724a-107">사용자의 Azure AD 계정으로 LCVista에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-107">You can enable your users to automatically get signed-on to LCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1724a-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1724a-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1724a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1724a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1724a-110">Prerequisites</span></span>

<span data-ttu-id="1724a-111">LCVista와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-111">To configure Azure AD integration with LCVista, you need the following items:</span></span>

- <span data-ttu-id="1724a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1724a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1724a-113">LCVista Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1724a-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1724a-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1724a-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1724a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1724a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1724a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1724a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1724a-118">Scenario description</span></span>
<span data-ttu-id="1724a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1724a-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1724a-121">갤러리에서 LCVista 추가</span><span class="sxs-lookup"><span data-stu-id="1724a-121">Adding LCVista from the gallery</span></span>
2. <span data-ttu-id="1724a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1724a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-the-gallery"></a><span data-ttu-id="1724a-123">갤러리에서 LCVista 추가</span><span class="sxs-lookup"><span data-stu-id="1724a-123">Adding LCVista from the gallery</span></span>
<span data-ttu-id="1724a-124">LCVista가 Azure AD에 통합되도록 구성하려면 갤러리에서 LCVista를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-124">To configure the integration of LCVista into Azure AD, you need to add LCVista from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1724a-125">**갤러리에서 LCVista를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1724a-125">**To add LCVista from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1724a-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1724a-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1724a-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1724a-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1724a-133">검색 상자에 **LCVista**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-133">In the search box, type **LCVista**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="1724a-135">결과 패널에서 **LCVista**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-135">In the results panel, select **LCVista**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1724a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1724a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1724a-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 LCVista에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1724a-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 대응하는 LCVista 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LCVista is to a user in Azure AD.</span></span> <span data-ttu-id="1724a-140">즉, Azure AD 사용자와 LCVista의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-140">In other words, a link relationship between an Azure AD user and the related user in LCVista needs to be established.</span></span>

<span data-ttu-id="1724a-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 LCVista의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LCVista.</span></span>

<span data-ttu-id="1724a-142">LCVista에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-142">To configure and test Azure AD single sign-on with LCVista, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1724a-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1724a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1724a-145">**[LCVista 테스트 사용자 만들기](#creating-a-lcvista-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 LCVista에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - to have a counterpart of Britta Simon in LCVista that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1724a-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1724a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1724a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1724a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1724a-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 LCVista 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="1724a-150">**LCVista에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1724a-150">**To configure Azure AD single sign-on with LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="1724a-151">Azure Portal의 **LCVista** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-151">In the Azure portal, on the **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1724a-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="1724a-155">**LCVista 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-155">On the **LCVista Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="1724a-157">a.</span><span class="sxs-lookup"><span data-stu-id="1724a-157">a.</span></span> <span data-ttu-id="1724a-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="1724a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="1724a-159">b.</span><span class="sxs-lookup"><span data-stu-id="1724a-159">b.</span></span> <span data-ttu-id="1724a-160">**식별자** 텍스트 상자에서 `https://<subdomain>.lcvista.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="1724a-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-161">These values are not the real.</span></span> <span data-ttu-id="1724a-162">실제 식별자 및 로그온 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-162">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="1724a-163">이러한 값을 얻으려면 [LCVista 클라이언트 지원 팀](https://lcvista.com/contact)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1724a-163">Contact [LCVista Client support team](https://lcvista.com/contact) to get these values.</span></span> 

4. <span data-ttu-id="1724a-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="1724a-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-166">Click **Save** button.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="1724a-168">**LCVista 구성** 섹션에서 **LCVista 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-168">On the **LCVista Configuration** section, click **Configure LCVista** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1724a-169">**빠른 참조 섹션**에서 **SAML 엔터티 ID** 및 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-169">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="1724a-171">LCVista 응용 프로그램에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-171">Sign on to your LCVista application as an administrator.</span></span>

8. <span data-ttu-id="1724a-172">**SAML Config(SAML 구성)** 섹션에서 **Enable SAML login(SAML 로그인 사용)**을 선택하고 아래 이미지의 설명에 따라 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-172">In the **SAML Config** section, check the **Enable SAML login** and enter the details as mentioned in below image.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="1724a-174">a.</span><span class="sxs-lookup"><span data-stu-id="1724a-174">a.</span></span> <span data-ttu-id="1724a-175">Azure AD에서 복사한 **발급자 URL**을 **Entity ID(엔터티 ID)** 섹션에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-175">Paste the **Issuer URL** which you have copied from Azure AD in the **Entity ID** section.</span></span> 

    <span data-ttu-id="1724a-176">b.</span><span class="sxs-lookup"><span data-stu-id="1724a-176">b.</span></span> <span data-ttu-id="1724a-177">Azure AD에서 복사한 **Single Sign-On 서비스 URL**을 **URL** 섹션에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-177">Paste the **Single Sign-On Service URL** which you have copied from Azure AD in the **URL** section.</span></span>

    <span data-ttu-id="1724a-178">c.</span><span class="sxs-lookup"><span data-stu-id="1724a-178">c.</span></span> <span data-ttu-id="1724a-179">Azure Portal에서 다운로드한 메타데이터(XML)에서 **X509Certificate** 값을 복사하여 **x509 Certificate(X509 인증서)** 섹션에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-179">From Metadata (XML) which you have downloaded from Azure portal, copy the value **X509Certificate** and paste it in the **x509 Certificate** section.</span></span>

    <span data-ttu-id="1724a-180">d.</span><span class="sxs-lookup"><span data-stu-id="1724a-180">d.</span></span> <span data-ttu-id="1724a-181">**First name attribute(이름 특성)** 텍스트 상자에 다음 값을 붙여 넣습니다. `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="1724a-181">In the **First name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="1724a-182">e.</span><span class="sxs-lookup"><span data-stu-id="1724a-182">e.</span></span> <span data-ttu-id="1724a-183">**Last name attribute(성 특성)** 텍스트 상자에 다음 값을 붙여 넣습니다. `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="1724a-183">In the **Last name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="1724a-184">f.</span><span class="sxs-lookup"><span data-stu-id="1724a-184">f.</span></span> <span data-ttu-id="1724a-185">**Email attribute(전자 메일 특성)** 텍스트 상자에 다음 값을 붙여 넣습니다. `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="1724a-185">In the **Email attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="1724a-186">g.</span><span class="sxs-lookup"><span data-stu-id="1724a-186">g.</span></span> <span data-ttu-id="1724a-187">**Username attribute(사용자 이름 특성)** 텍스트 상자에 다음 값을 붙여 넣습니다. `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="1724a-187">In the **Username attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="1724a-188">e.</span><span class="sxs-lookup"><span data-stu-id="1724a-188">e.</span></span> <span data-ttu-id="1724a-189">**저장**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-189">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="1724a-190">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1724a-191">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1724a-192">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1724a-193">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1724a-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="1724a-194">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1724a-196">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="1724a-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1724a-197">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1724a-199">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1724a-201">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1724a-203">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1724a-205">a.</span><span class="sxs-lookup"><span data-stu-id="1724a-205">a.</span></span> <span data-ttu-id="1724a-206">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1724a-207">b.</span><span class="sxs-lookup"><span data-stu-id="1724a-207">b.</span></span> <span data-ttu-id="1724a-208">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1724a-209">c.</span><span class="sxs-lookup"><span data-stu-id="1724a-209">c.</span></span> <span data-ttu-id="1724a-210">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1724a-211">d.</span><span class="sxs-lookup"><span data-stu-id="1724a-211">d.</span></span> <span data-ttu-id="1724a-212">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="1724a-213">LCVista 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1724a-213">Creating a LCVista test user</span></span>

<span data-ttu-id="1724a-214">이 섹션에서는 LCVista에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="1724a-215">LCVista 응용 프로그램에 사용자를 추가하려면 [LCVista 클라이언트 지원 팀](https://lcvista.com/contact)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-215">You need to contact [LCVista Client support team](https://lcvista.com/contact) to add the users in the LCVista application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1724a-216">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1724a-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1724a-217">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 LCVista에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LCVista.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1724a-219">**Britta Simon을 LCVista에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1724a-219">**To assign Britta Simon to LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="1724a-220">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1724a-222">응용 프로그램 목록에서 **LCVista**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-222">In the applications list, select **LCVista**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="1724a-224">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-224">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1724a-226">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-226">Click **Add** button.</span></span> <span data-ttu-id="1724a-227">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1724a-229">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1724a-230">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1724a-231">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1724a-232">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1724a-232">Testing single sign-on</span></span>

<span data-ttu-id="1724a-233">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="1724a-234">액세스 패널에서 LCVista 타일을 클릭하면 조직 로그온 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-234">Click the LCVista tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="1724a-235">로그인이 성공한 후 LCVista 응용 프로그램에 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="1724a-235">After successful login, you will be signed-on to your LCVista application.</span></span> <span data-ttu-id="1724a-236">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1724a-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1724a-237">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1724a-237">Additional resources</span></span>

* [<span data-ttu-id="1724a-238">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="1724a-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1724a-239">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1724a-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png


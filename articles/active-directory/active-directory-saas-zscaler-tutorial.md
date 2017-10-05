---
title: "자습서: Azure Active Directory와 Zscaler 통합| Microsoft Docs"
description: "Azure Active Directory와 Zscaler 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 73c81691b68ee820e1d905a17b4f2ab6b6ceb5fd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="301de-103">자습서: Azure Active Directory와 Zscaler 통합</span><span class="sxs-lookup"><span data-stu-id="301de-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="301de-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Zscaler를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="301de-104">In this tutorial, you learn how to integrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="301de-105">Zscaler를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="301de-105">Integrating Zscaler with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="301de-106">Zscaler에 액세스할 수 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-106">You can control in Azure AD who has access to Zscaler</span></span>
- <span data-ttu-id="301de-107">사용자가 자신의 Azure AD 계정으로 Zscaler에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-107">You can enable your users to automatically get signed-on to Zscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="301de-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="301de-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="301de-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="301de-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="301de-110">Prerequisites</span></span>

<span data-ttu-id="301de-111">Zscaler와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-111">To configure Azure AD integration with Zscaler, you need the following items:</span></span>

- <span data-ttu-id="301de-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="301de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="301de-113">Zscaler Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="301de-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="301de-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="301de-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="301de-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="301de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="301de-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="301de-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="301de-118">Scenario description</span></span>
<span data-ttu-id="301de-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="301de-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="301de-121">갤러리에서 Zscaler 추가</span><span class="sxs-lookup"><span data-stu-id="301de-121">Adding Zscaler from the gallery</span></span>
2. <span data-ttu-id="301de-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="301de-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-the-gallery"></a><span data-ttu-id="301de-123">갤러리에서 Zscaler 추가</span><span class="sxs-lookup"><span data-stu-id="301de-123">Adding Zscaler from the gallery</span></span>
<span data-ttu-id="301de-124">Zscaler가 Azure AD에 통합되도록 구성하려면 갤러리의 Zscaler를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-124">To configure the integration of Zscaler into Azure AD, you need to add Zscaler from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="301de-125">**갤러리에서 Zscaler를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="301de-125">**To add Zscaler from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="301de-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="301de-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="301de-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="301de-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="301de-133">검색 상자에 **Zscaler**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-133">In the search box, type **Zscaler**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. <span data-ttu-id="301de-135">결과 패널에서 **Zscaler**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-135">In the results panel, select **Zscaler**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="301de-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="301de-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="301de-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Zscaler에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="301de-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Zscaler 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler is to a user in Azure AD.</span></span> <span data-ttu-id="301de-140">즉, Azure AD 사용자와 Zscaler의 관련 사용자 간에 연결 관계를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler needs to be established.</span></span>

<span data-ttu-id="301de-141">Zscaler에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-141">In Zscaler, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="301de-142">Zscaler에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-142">To configure and test Azure AD single sign-on with Zscaler, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="301de-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="301de-144">**[프록시 설정 구성](#configuring-proxy-settings)** - Internet Explorer에서 프록시 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="301de-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="301de-146">**[Zscaler 테스트 사용자 만들기](#creating-a-zscaler-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Zscaler에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="301de-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - to have a counterpart of Britta Simon in Zscaler that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="301de-147">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="301de-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="301de-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="301de-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="301de-150">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Zscaler 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="301de-151">**Zscaler에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="301de-151">**To configure Azure AD single sign-on with Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="301de-152">Azure Portal의 **Zscaler** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-152">In the Azure portal, on the **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="301de-154">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. <span data-ttu-id="301de-156">**Zscaler 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-156">On the **Zscaler Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="301de-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.zsclaer.net`</span><span class="sxs-lookup"><span data-stu-id="301de-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="301de-159">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="301de-159">This value is not real.</span></span> <span data-ttu-id="301de-160">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="301de-161">이 값을 얻으려면 [Zscaler 클라이언트 지원 팀](https://www.zscaler.com/company/contact)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="301de-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) to get this value.</span></span> 

4. <span data-ttu-id="301de-162">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. <span data-ttu-id="301de-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-164">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="301de-166">**Zscaler 구성** 섹션에서 **Zscaler 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="301de-166">On the **Zscaler Configuration** section, click **Configure Zscaler** to open **Configure sign-on** window.</span></span> <span data-ttu-id="301de-167">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. <span data-ttu-id="301de-169">다른 웹 브라우저 창에서 ZScaler 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-169">In a different web browser window, log in to your ZScaler company site as an administrator.</span></span>

8. <span data-ttu-id="301de-170">위쪽의 메뉴에서 **관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-170">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="301de-171">![관리](./media/active-directory-saas-zscaler-tutorial/ic800206.png "관리")</span><span class="sxs-lookup"><span data-stu-id="301de-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="301de-172">**관리자 & 역할 관리**에서 **사용자 및 인증 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="301de-173">![사용자 및 인증 관리](./media/active-directory-saas-zscaler-tutorial/ic800207.png "사용자 및 인증 관리")</span><span class="sxs-lookup"><span data-stu-id="301de-173">![Manage Users & Authentication](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="301de-174">**구성에 대한 인증 옵션 선택** 섹션에서, 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-174">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="301de-175">![인증](./media/active-directory-saas-zscaler-tutorial/ic800208.png "인증")</span><span class="sxs-lookup"><span data-stu-id="301de-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="301de-176">a.</span><span class="sxs-lookup"><span data-stu-id="301de-176">a.</span></span> <span data-ttu-id="301de-177">**SAML Single Sign-On을 사용하여 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="301de-178">b.</span><span class="sxs-lookup"><span data-stu-id="301de-178">b.</span></span> <span data-ttu-id="301de-179">**SAML Single Sign-On 매개 변수 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="301de-180">**SAML Single Sign-On 매개 변수 구성** 대화 상자 페이지에서 다음 단계를 수행하고 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-180">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="301de-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="301de-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="301de-182">a.</span><span class="sxs-lookup"><span data-stu-id="301de-182">a.</span></span> <span data-ttu-id="301de-183">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **URL of the SAML Portal to which users are sent for authentication**(인증할 사용자가 전송되는 SAML 포털의 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-183">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="301de-184">b.</span><span class="sxs-lookup"><span data-stu-id="301de-184">b.</span></span> <span data-ttu-id="301de-185">**로그인 이름을 포함한 특성** 텍스트 상자에 **NameID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-185">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="301de-186">c.</span><span class="sxs-lookup"><span data-stu-id="301de-186">c.</span></span> <span data-ttu-id="301de-187">**Zscaler pem**을 클릭하여 다운로드한 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-187">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="301de-188">d.</span><span class="sxs-lookup"><span data-stu-id="301de-188">d.</span></span> <span data-ttu-id="301de-189">**SAML 자동 프로비전 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-189">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="301de-190">**사용자 인증 구성** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-190">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="301de-191">![관리](./media/active-directory-saas-zscaler-tutorial/ic800210.png "관리")</span><span class="sxs-lookup"><span data-stu-id="301de-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="301de-192">a.</span><span class="sxs-lookup"><span data-stu-id="301de-192">a.</span></span> <span data-ttu-id="301de-193">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-193">Click **Save**.</span></span>

    <span data-ttu-id="301de-194">b.</span><span class="sxs-lookup"><span data-stu-id="301de-194">b.</span></span> <span data-ttu-id="301de-195">**지금 활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="301de-196">프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="301de-196">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="301de-197">Internet Explorer에서 프록시 설정을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="301de-197">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="301de-198">**Internet Explorer**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-198">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="301de-199">**도구** 메뉴에서 **인터넷 옵션**을 선택하여 **인터넷 옵션** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="301de-199">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="301de-200">![인터넷 옵션](./media/active-directory-saas-zscaler-tutorial/ic769492.png "인터넷 옵션")</span><span class="sxs-lookup"><span data-stu-id="301de-200">![Internet Options](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="301de-201">**연결** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-201">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="301de-202">![연결](./media/active-directory-saas-zscaler-tutorial/ic769493.png "연결")</span><span class="sxs-lookup"><span data-stu-id="301de-202">![Connections](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="301de-203">**LAN 설정**을 클릭하여 **LAN 설정** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="301de-203">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="301de-204">프록시 서버 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-204">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="301de-205">![프록시 서버](./media/active-directory-saas-zscaler-tutorial/ic769494.png "프록시 서버")</span><span class="sxs-lookup"><span data-stu-id="301de-205">![Proxy server](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="301de-206">a.</span><span class="sxs-lookup"><span data-stu-id="301de-206">a.</span></span> <span data-ttu-id="301de-207">**사용자 LAN의 프록시 서버 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="301de-208">b.</span><span class="sxs-lookup"><span data-stu-id="301de-208">b.</span></span> <span data-ttu-id="301de-209">[주소] 텍스트 상자에 **gateway.zscaler.net**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-209">In the Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="301de-210">c.</span><span class="sxs-lookup"><span data-stu-id="301de-210">c.</span></span> <span data-ttu-id="301de-211">포트 텍스트 상자에 **80**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-211">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="301de-212">d.</span><span class="sxs-lookup"><span data-stu-id="301de-212">d.</span></span> <span data-ttu-id="301de-213">**로컬 주소의 바이패스 프록시 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="301de-214">e.</span><span class="sxs-lookup"><span data-stu-id="301de-214">e.</span></span> <span data-ttu-id="301de-215">**확인**을 클릭하여 **LAN(Local Area Network) 설정** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-215">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="301de-216">**확인**을 클릭하여 **인터넷 옵션** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-216">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="301de-217">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-217">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="301de-218">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="301de-218">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="301de-219">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-219">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="301de-220">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="301de-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="301de-221">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="301de-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="301de-223">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="301de-223">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="301de-224">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-224">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="301de-226">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-226">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="301de-228">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-228">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="301de-230">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-230">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="301de-232">a.</span><span class="sxs-lookup"><span data-stu-id="301de-232">a.</span></span> <span data-ttu-id="301de-233">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-233">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="301de-234">b.</span><span class="sxs-lookup"><span data-stu-id="301de-234">b.</span></span> <span data-ttu-id="301de-235">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-235">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="301de-236">c.</span><span class="sxs-lookup"><span data-stu-id="301de-236">c.</span></span> <span data-ttu-id="301de-237">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="301de-237">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="301de-238">d.</span><span class="sxs-lookup"><span data-stu-id="301de-238">d.</span></span> <span data-ttu-id="301de-239">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="301de-240">Zscaler 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="301de-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="301de-241">Azure AD 사용자가 ZScaler에 로그인할 수 있도록 하려면 ZScaler로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-241">To enable Azure AD users to log in to ZScaler, they must be provisioned to ZScaler.</span></span>  
<span data-ttu-id="301de-242">ZScaler의 경우, 수동으로 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-242">In the case of ZScaler, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="301de-243">사용자 프로비저닝을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="301de-243">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="301de-244">**Zscaler** 테넌트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-244">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="301de-245">**관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="301de-246">![관리](./media/active-directory-saas-zscaler-tutorial/ic781035.png "관리")</span><span class="sxs-lookup"><span data-stu-id="301de-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="301de-247">**사용자 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="301de-248">![추가](./media/active-directory-saas-zscaler-tutorial/ic781036.png "추가")</span><span class="sxs-lookup"><span data-stu-id="301de-248">![Add](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="301de-249">**사용자** 탭에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-249">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="301de-250">![추가](./media/active-directory-saas-zscaler-tutorial/ic781037.png "추가")</span><span class="sxs-lookup"><span data-stu-id="301de-250">![Add](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="301de-251">사용자 추가 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-251">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="301de-252">![사용자 추가](./media/active-directory-saas-zscaler-tutorial/ic781038.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="301de-252">![Add User](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="301de-253">a.</span><span class="sxs-lookup"><span data-stu-id="301de-253">a.</span></span> <span data-ttu-id="301de-254">**사용자ID**, **사용자 표시 이름**, **암호**, **암호 확인**을 입력하고, 프로비전하고자 하는 유효한 AAD 계정의 **그룹** 및 **부서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-254">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="301de-255">b.</span><span class="sxs-lookup"><span data-stu-id="301de-255">b.</span></span> <span data-ttu-id="301de-256">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="301de-257">다른 ZScaler 사용자 계정 생성 도구 또는 ZScaler에서 제공하는 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="301de-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="301de-258">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="301de-258">Assigning the Azure AD test user</span></span>

<span data-ttu-id="301de-259">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Zscaler에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-259">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler.</span></span>

![사용자 할당][200] 

<span data-ttu-id="301de-261">**Britta Simon을 Zscaler에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="301de-261">**To assign Britta Simon to Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="301de-262">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-262">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="301de-264">응용 프로그램 목록에서 **Zscaler**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-264">In the applications list, select **Zscaler**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. <span data-ttu-id="301de-266">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-266">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="301de-268">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-268">Click **Add** button.</span></span> <span data-ttu-id="301de-269">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="301de-271">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-271">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="301de-272">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-272">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="301de-273">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="301de-274">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="301de-274">Testing single sign-on</span></span>

<span data-ttu-id="301de-275">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="301de-275">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="301de-276">액세스 패널에서 Zscaler 타일을 클릭하면 Zscaler 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="301de-276">When you click the Zscaler tile in the Access Panel, you should get automatically signed-on to your Zscaler application.</span></span>
<span data-ttu-id="301de-277">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="301de-277">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="301de-278">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="301de-278">Additional resources</span></span>

* [<span data-ttu-id="301de-279">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="301de-279">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="301de-280">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="301de-280">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png


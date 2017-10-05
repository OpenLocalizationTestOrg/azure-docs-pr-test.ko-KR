---
title: "자습서: xMatters OnDemand와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 xMatters OnDemand 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9bfcb44ed19f167872b3cd9119e2dbdd35c82604
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="1986c-103">자습서: xMatters OnDemand와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1986c-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="1986c-104">이 자습서에서는 Azure AD(Azure Active Directory)와 xMatters OnDemand를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-104">In this tutorial, you learn how to integrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1986c-105">xMatters OnDemand를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-105">Integrating xMatters OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1986c-106">xMatters OnDemand에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-106">You can control in Azure AD who has access to xMatters OnDemand</span></span>
- <span data-ttu-id="1986c-107">사용자가 자신의 Azure AD 계정으로 xMatters OnDemand에 자동으로 로그온(Single Sign-On) 되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-107">You can enable your users to automatically get signed-on to xMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1986c-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1986c-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1986c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1986c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1986c-110">Prerequisites</span></span>

<span data-ttu-id="1986c-111">xMatters OnDemand와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-111">To configure Azure AD integration with xMatters OnDemand, you need the following items:</span></span>

- <span data-ttu-id="1986c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1986c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1986c-113">xMatters OnDemand Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1986c-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1986c-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1986c-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1986c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1986c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1986c-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1986c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1986c-118">Scenario description</span></span>
<span data-ttu-id="1986c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1986c-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1986c-121">갤러리에서 xMatters OnDemand 추가</span><span class="sxs-lookup"><span data-stu-id="1986c-121">Adding xMatters OnDemand from the gallery</span></span>
2. <span data-ttu-id="1986c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1986c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-the-gallery"></a><span data-ttu-id="1986c-123">갤러리에서 xMatters OnDemand 추가</span><span class="sxs-lookup"><span data-stu-id="1986c-123">Adding xMatters OnDemand from the gallery</span></span>
<span data-ttu-id="1986c-124">xMatters OnDemand가 Azure AD에 통합되도록 구성하려면 갤러리에서 xMatters OnDemand를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-124">To configure the integration of xMatters OnDemand into Azure AD, you need to add xMatters OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1986c-125">**갤러리에서 xMatters OnDemand를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1986c-125">**To add xMatters OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1986c-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1986c-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1986c-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1986c-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1986c-133">검색 상자에 **xMatters OnDemand**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-133">In the search box, type **xMatters OnDemand**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="1986c-135">결과 패널에서 **xMatters OnDemand**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-135">In the results panel, select **xMatters OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1986c-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1986c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1986c-138">이 섹션에서는 Britta Simon이라는 테스트 사용자를 기반으로 xMatters OnDemand에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1986c-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 xMatters OnDemand 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in xMatters OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="1986c-140">즉, Azure AD 사용자와 xMatters OnDemand의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-140">In other words, a link relationship between an Azure AD user and the related user in xMatters OnDemand needs to be established.</span></span>

<span data-ttu-id="1986c-141">xMatters OnDemand에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-141">In xMatters OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1986c-142">xMatters OnDemand에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-142">To configure and test Azure AD single sign-on with xMatters OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1986c-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1986c-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1986c-145">**[xMatters OnDemand 테스트 사용자 만들기](#creating-a-xmatters-ondemand-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 해당 사용자를 xMatters OnDemand에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - to have a counterpart of Britta Simon in xMatters OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1986c-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1986c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1986c-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1986c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1986c-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 xMatters OnDemand 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="1986c-150">**xMatters OnDemand에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1986c-150">**To configure Azure AD single sign-on with xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="1986c-151">Azure Portal의 **xMatters OnDemand** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-151">In the Azure portal, on the **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1986c-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="1986c-155">**xMatters OnDemand 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-155">On the **xMatters OnDemand Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="1986c-157">a.</span><span class="sxs-lookup"><span data-stu-id="1986c-157">a.</span></span> <span data-ttu-id="1986c-158">**식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="1986c-159">b.</span><span class="sxs-lookup"><span data-stu-id="1986c-159">b.</span></span> <span data-ttu-id="1986c-160">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="1986c-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-161">These values are not real.</span></span> <span data-ttu-id="1986c-162">실제 식별자 및 회신 URL로 해당 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="1986c-163">이러한 값을 얻으려면 [xMatters OnDemand 지원 팀](https://www.xmatters.com/company/contact-us/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1986c-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="1986c-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 인증서 파일을 로컬에 **c:\\XMatters OnDemand.cer**으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="1986c-166">인증서를 [xMatters OnDemand 지원 팀](https://www.xmatters.com/company/contact-us/)에 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-166">You need to forward the certificate to the [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="1986c-167">Single Sign-On 구성을 완료하기 전에 xMatters 지원팀에서 인증서를 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-167">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span></span> 

5. <span data-ttu-id="1986c-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1986c-170">**xMatters OnDemand 구성** 섹션에서 **xMatters OnDemand 구성**을 클릭하여 **로그인 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-170">On the **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1986c-171">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="1986c-173">다른 웹 브라우저 창에서 XMatters OnDemand 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-173">In a different web browser window, log in to your XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="1986c-174">위쪽에 도구 모음에서 **관리자**를 클릭한 후 왼쪽 탐색 모음에서 **회사 세부 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-174">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span></span>
   
    <span data-ttu-id="1986c-175">![관리자](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="1986c-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="1986c-176">**SAML 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-176">On the **SAML Configuration** page, perform the following steps:</span></span>
   
    <span data-ttu-id="1986c-177">![SAML 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML 구성")</span><span class="sxs-lookup"><span data-stu-id="1986c-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="1986c-178">a.</span><span class="sxs-lookup"><span data-stu-id="1986c-178">a.</span></span> <span data-ttu-id="1986c-179">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="1986c-180">b.</span><span class="sxs-lookup"><span data-stu-id="1986c-180">b.</span></span> <span data-ttu-id="1986c-181">Azure Portal에서 복사한 **SAML 엔터티 ID**를 **ID 공급자 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-181">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="1986c-182">c.</span><span class="sxs-lookup"><span data-stu-id="1986c-182">c.</span></span> <span data-ttu-id="1986c-183">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **Single Sign-On URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="1986c-184">d.</span><span class="sxs-lookup"><span data-stu-id="1986c-184">d.</span></span> <span data-ttu-id="1986c-185">Azure Portal에서 복사한 **로그아웃 URL**을 **Single Logout URL**(단일 로그아웃 URL) 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="1986c-186">e.</span><span class="sxs-lookup"><span data-stu-id="1986c-186">e.</span></span> <span data-ttu-id="1986c-187">회사 상세 정보 페이지 위쪽에서 **변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-187">On the Company Details page, at the top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="1986c-188">![회사 상세 정보](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "회사 상세 정보")</span><span class="sxs-lookup"><span data-stu-id="1986c-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="1986c-189">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1986c-190">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1986c-191">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1986c-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1986c-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="1986c-193">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1986c-195">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="1986c-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1986c-196">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1986c-198">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1986c-200">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1986c-202">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1986c-204">a.</span><span class="sxs-lookup"><span data-stu-id="1986c-204">a.</span></span> <span data-ttu-id="1986c-205">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1986c-206">b.</span><span class="sxs-lookup"><span data-stu-id="1986c-206">b.</span></span> <span data-ttu-id="1986c-207">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1986c-208">c.</span><span class="sxs-lookup"><span data-stu-id="1986c-208">c.</span></span> <span data-ttu-id="1986c-209">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1986c-210">d.</span><span class="sxs-lookup"><span data-stu-id="1986c-210">d.</span></span> <span data-ttu-id="1986c-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="1986c-212">xMatters OnDemand 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1986c-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="1986c-213">Azure AD 사용자가 XMatters OnDemand에 로그인할 수 있도록 하려면 XMatters OnDemand로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-213">In order to enable Azure AD users to log in to XMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="1986c-214">XMatters OnDemand의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-214">In the case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="1986c-215">사용자 계정을 프로비저닝하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-215">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="1986c-216">**XMatters OnDemand** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-216">Log in to your **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="1986c-217">**사용자** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-217">Click **Users** tab.</span></span> <span data-ttu-id="1986c-218">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-218">and then click **Add User**.</span></span>
  
    <span data-ttu-id="1986c-219">![사용자](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="1986c-219">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="1986c-220">**사용자 추가** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-220">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1986c-221">![사용자 추가](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="1986c-221">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="1986c-222">a.</span><span class="sxs-lookup"><span data-stu-id="1986c-222">a.</span></span> <span data-ttu-id="1986c-223">**활성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-223">Select **Active**.</span></span>

    <span data-ttu-id="1986c-224">b.</span><span class="sxs-lookup"><span data-stu-id="1986c-224">b.</span></span> <span data-ttu-id="1986c-225">**사용자 ID** 텍스트 상자에 사용자의 ID(예: Brittasimon@contoso.com)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-225">In the **User ID** textbox, type the user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="1986c-226">c.</span><span class="sxs-lookup"><span data-stu-id="1986c-226">c.</span></span> <span data-ttu-id="1986c-227">**이름** 텍스트 상자에 사용자의 이름(예: Britta)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-227">In the **First Name** textbox, type first name of the user like Britta.</span></span>

    <span data-ttu-id="1986c-228">d.</span><span class="sxs-lookup"><span data-stu-id="1986c-228">d.</span></span> <span data-ttu-id="1986c-229">**성** 텍스트 상자에 사용자의 성(예: Simon)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-229">In the **Last Name** textbox, type last name of the user like Simon.</span></span>
    
    <span data-ttu-id="1986c-230">e.</span><span class="sxs-lookup"><span data-stu-id="1986c-230">e.</span></span> <span data-ttu-id="1986c-231">**사이트** 텍스트 상자에 프로비전하려는 유효한 Azure AD의 계정의 유요한 사이트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-231">In the **Site** textbox, Enter the valid site of a valid Azure AD account you want to provision.</span></span>
    
    <span data-ttu-id="1986c-232">f.</span><span class="sxs-lookup"><span data-stu-id="1986c-232">f.</span></span> <span data-ttu-id="1986c-233">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-233">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1986c-234">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1986c-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1986c-235">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 xMatters OnDemand에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to xMatters OnDemand.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1986c-237">**Britta Simon을 xMatters OnDemand에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="1986c-237">**To assign Britta Simon to xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="1986c-238">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1986c-240">응용 프로그램 목록에서 **xMatters OnDemand**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-240">In the applications list, select **xMatters OnDemand**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="1986c-242">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-242">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1986c-244">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-244">Click **Add** button.</span></span> <span data-ttu-id="1986c-245">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1986c-247">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1986c-248">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1986c-249">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1986c-250">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1986c-250">Testing single sign-on</span></span>

<span data-ttu-id="1986c-251">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1986c-252">액세스 패널에서 xMatters OnDemand 타일을 클릭하면 xMatters OnDemand 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="1986c-252">When you click the xMatters OnDemand tile in the Access Panel, you should get automatically signed-on to your xMatters OnDemand application.</span></span>
<span data-ttu-id="1986c-253">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1986c-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1986c-254">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1986c-254">Additional resources</span></span>

* [<span data-ttu-id="1986c-255">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="1986c-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1986c-256">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1986c-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png


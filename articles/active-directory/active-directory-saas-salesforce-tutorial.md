---
title: "자습서: Salesforce와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Salesforce 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 639e40ca7e406a1726033e9f5c5363c289087589
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="c4435-103">자습서: Salesforce와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c4435-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="c4435-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Salesforce를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4435-105">Salesforce를 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c4435-106">Salesforce에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-106">You can control in Azure AD who has access to Salesforce</span></span>
- <span data-ttu-id="c4435-107">사용자가 해당 Azure AD 계정으로 Salesforce에 자동으로 로그인(Single Sign-On)하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4435-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c4435-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4435-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4435-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c4435-110">Prerequisites</span></span>

<span data-ttu-id="c4435-111">Salesforce와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-111">To configure Azure AD integration with Salesforce, you need the following items:</span></span>

- <span data-ttu-id="c4435-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c4435-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4435-113">Salesforce Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c4435-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4435-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4435-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4435-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c4435-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4435-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4435-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c4435-118">Scenario description</span></span>
<span data-ttu-id="c4435-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4435-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4435-121">갤러리에서 Salesforce 추가</span><span class="sxs-lookup"><span data-stu-id="c4435-121">Adding Salesforce from the gallery</span></span>
2. <span data-ttu-id="c4435-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c4435-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-the-gallery"></a><span data-ttu-id="c4435-123">갤러리에서 Salesforce 추가</span><span class="sxs-lookup"><span data-stu-id="c4435-123">Adding Salesforce from the gallery</span></span>
<span data-ttu-id="c4435-124">Salesforce의 Azure AD 통합을 구성하려면 갤러리의 Salesforce를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c4435-125">**갤러리에서 Salesforce를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c4435-125">**To add Salesforce from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c4435-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4435-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c4435-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c4435-131">대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-131">Click **New application** button on the top of the dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c4435-133">검색 상자에 **Salesforce**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-133">In the search box, type **Salesforce**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="c4435-135">결과 창에서 **Salesforce**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-135">In the results panel, select **Salesforce**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4435-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c4435-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4435-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Salesforce에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c4435-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Salesforce 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span></span> <span data-ttu-id="c4435-140">즉, Azure AD 사용자와 Salesforce의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span></span>

<span data-ttu-id="c4435-141">이 연결 관계는 Azure AD의 **사용자 이름** 값을 Salesforce의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce.</span></span>

<span data-ttu-id="c4435-142">Salesforce에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-142">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c4435-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c4435-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4435-145">**[Salesforce 테스트 사용자 만들기](#creating-a-salesforce-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Salesforce에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4435-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4435-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4435-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c4435-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4435-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Salesforce 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="c4435-150">**Salesforce에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c4435-150">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="c4435-151">Azure Portal의 **Salesforce** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-151">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c4435-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="c4435-155">**Salesforce 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-155">On the **Salesforce Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="c4435-157">**로그온 URL** 텍스트 상자에 다음 패턴으로 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-157">In the **Sign-on URL** textbox, type the value using the following pattern:</span></span> 
   * <span data-ttu-id="c4435-158">엔터프라이즈 계정: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c4435-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="c4435-159">개발자 계정: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c4435-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4435-160">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-160">These values are not the real.</span></span> <span data-ttu-id="c4435-161">이러한 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-161">Update these values with the actual Sign-on URL.</span></span> <span data-ttu-id="c4435-162">이러한 값을 얻으려면 [Salesforce 클라이언트 지원 팀](https://help.salesforce.com/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="c4435-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="c4435-163">**SAML 서명 인증서** 섹션에서 **인증서**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-163">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="c4435-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-165">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4435-167">**Salesforce 구성** 섹션에서 **Salesforce 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-167">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c4435-168">**빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    <span data-ttu-id="c4435-169">![Single Sign-On 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="c4435-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="c4435-170">브라우저에서 새 탭을 열고 Salesforce 관리자 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-170">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>

8.  <span data-ttu-id="c4435-171">**관리자** 탐색 창에서 **보안 제어**를 클릭하여 관련된 섹션을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-171">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span></span> <span data-ttu-id="c4435-172">그런 다음 **Single Sign-On 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-172">Then click **Single Sign-On Settings**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="c4435-174">**Single Sign-on 설정** 페이지에서 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-174">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>
    <span data-ttu-id="c4435-175">![Single Sign-On 구성](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="c4435-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="c4435-176">Salesforce 계정에 Single Sign-On을 사용하도록 설정할 수 없는 경우 [Salesforce 클라이언트 지원 팀](https://help.salesforce.com/support)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-176">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="c4435-177">**SAML 사용**을 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="c4435-179">SAML Single Sign-On 설정을 구성하려면 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-179">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="c4435-181">**SAML Single Sign-on 설정 편집** 페이지에서 다음 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-181">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="c4435-183">a.</span><span class="sxs-lookup"><span data-stu-id="c4435-183">a.</span></span> <span data-ttu-id="c4435-184">**이름** 필드에 이 구성에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-184">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="c4435-185">**이름**에 값을 제공하면 **API 이름** 입력란이 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-185">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>

    <span data-ttu-id="c4435-186">b.</span><span class="sxs-lookup"><span data-stu-id="c4435-186">b.</span></span> <span data-ttu-id="c4435-187">**SMAL 엔터티 ID** 값을 Salesforce의 **발급자** 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-187">Paste **SMAL Entity ID** value into the **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="c4435-188">c.</span><span class="sxs-lookup"><span data-stu-id="c4435-188">c.</span></span> <span data-ttu-id="c4435-189">**엔터티 ID**입력란에 다음 패턴을 사용하여 Salesforce 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-189">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>
      
      * <span data-ttu-id="c4435-190">엔터프라이즈 계정: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c4435-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="c4435-191">개발자 계정: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c4435-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="c4435-192">d.</span><span class="sxs-lookup"><span data-stu-id="c4435-192">d.</span></span> <span data-ttu-id="c4435-193">**찾아보기** 또는 **파일 선택**을 클릭하여 **업로드할 파일 선택** 대화 상자를 열고, Salesforce 인증서를 선택한 다음, **열기**를 클릭하여 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-193">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="c4435-194">e.</span><span class="sxs-lookup"><span data-stu-id="c4435-194">e.</span></span> <span data-ttu-id="c4435-195">**SAML ID 형식**에서 **어설션에 사용자의 salesforce.com 사용자 이름 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="c4435-196">f.</span><span class="sxs-lookup"><span data-stu-id="c4435-196">f.</span></span> <span data-ttu-id="c4435-197">**SAML ID 위치**에서 **Subject 문의 NameIdentifier 요소에 ID 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-197">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span></span>

    <span data-ttu-id="c4435-198">g.</span><span class="sxs-lookup"><span data-stu-id="c4435-198">g.</span></span> <span data-ttu-id="c4435-199">**Single Sign-On 서비스 URL**을 Salesforce의 **ID 공급자 로그인 URL** 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-199">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="c4435-200">h.</span><span class="sxs-lookup"><span data-stu-id="c4435-200">h.</span></span> <span data-ttu-id="c4435-201">**서비스 공급자가 시작한 요청 바인딩**에서 **HTTP 리디렉션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="c4435-202">i.</span><span class="sxs-lookup"><span data-stu-id="c4435-202">i.</span></span> <span data-ttu-id="c4435-203">마지막으로 **저장**을 클릭하여 SAML Single Sign-On 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-203">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="c4435-204">Salesforce에서 왼쪽 탐색 창에서 **도메인 관리**를 클릭하여 관련된 섹션을 확장한 다음 **내 도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-204">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="c4435-206">**인증 구성** 섹션으로 스크롤하여 **편집** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-206">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="c4435-208">**인증 서비스**섹션에서 SAML SSO 구성 이름을 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-208">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="c4435-210">둘 이상의 인증 서비스를 선택하는 경우 사용자가 Salesforce 환경으로 Single Sign-On을 시작하면 로그인하려는 인증 서비스를 선택하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-210">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span></span> <span data-ttu-id="c4435-211">이 메시지가 표시되지 않도록 하려면 **다른 모든 인증 서비스를 선택하지 않은 상태로 유지**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-211">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="c4435-212">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c4435-213">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c4435-214">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4435-215">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c4435-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4435-216">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c4435-218">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="c4435-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c4435-219">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-219">On the left navigation pane in the **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4435-221">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-221">To display the list of users, Go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4435-223">대화 상자 위쪽에서 **추가**를 클릭하여 **사용자** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-223">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4435-225">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4435-227">a.</span><span class="sxs-lookup"><span data-stu-id="c4435-227">a.</span></span> <span data-ttu-id="c4435-228">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4435-229">b.</span><span class="sxs-lookup"><span data-stu-id="c4435-229">b.</span></span> <span data-ttu-id="c4435-230">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4435-231">c.</span><span class="sxs-lookup"><span data-stu-id="c4435-231">c.</span></span> <span data-ttu-id="c4435-232">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c4435-233">d.</span><span class="sxs-lookup"><span data-stu-id="c4435-233">d.</span></span> <span data-ttu-id="c4435-234">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="c4435-235">Salesforce 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c4435-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="c4435-236">이 섹션에서는 Salesforce에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="c4435-237">Salesforce는 기본적으로 설정되는 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="c4435-238">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-238">There is no action item for you in this section.</span></span> <span data-ttu-id="c4435-239">Salesforce에 사용자가 없는 경우 Salesforce에 액세스하려고 시도하면 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c4435-240">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="c4435-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c4435-241">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Salesforce에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c4435-243">**Salesforce에 사용자를 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="c4435-243">**To assign Britta Simon to Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="c4435-244">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c4435-246">응용 프로그램 목록에서 **Salesforce**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-246">In the applications list, select **Salesforce**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="c4435-248">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-248">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c4435-250">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-250">Click **Add** button.</span></span> <span data-ttu-id="c4435-251">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c4435-253">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c4435-254">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4435-255">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4435-256">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c4435-256">Testing single sign-on</span></span>

<span data-ttu-id="c4435-257">Single Sign-On 설정을 테스트하려면 [https://myapps.microsoft.com](https://myapps.microsoft.com/)에서 액세스 패널을 연 다음 테스트 계정에 로그인하고 **Salesforce**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4435-257">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4435-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c4435-258">Additional resources</span></span>

* [<span data-ttu-id="c4435-259">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="c4435-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4435-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c4435-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c4435-261">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="c4435-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png


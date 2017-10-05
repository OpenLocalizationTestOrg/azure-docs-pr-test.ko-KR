---
title: "자습서: Syncplicity와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Syncplicity 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 1321fa71bcd625d6ea754432bfb402d3919e38f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="802bc-103">자습서: Syncplicity와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="802bc-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="802bc-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Syncplicity를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-104">In this tutorial, you learn how to integrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="802bc-105">Syncplicity와 Azure AD를 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-105">Integrating Syncplicity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="802bc-106">Syncplicity에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-106">You can control in Azure AD who has access to Syncplicity</span></span>
- <span data-ttu-id="802bc-107">사용자가 해당 Azure AD 계정으로 Syncplicity에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-107">You can enable your users to automatically get signed-on to Syncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="802bc-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="802bc-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="802bc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="802bc-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="802bc-110">Prerequisites</span></span>

<span data-ttu-id="802bc-111">Syncplicity와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-111">To configure Azure AD integration with Syncplicity, you need the following items:</span></span>

- <span data-ttu-id="802bc-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="802bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="802bc-113">Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="802bc-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="802bc-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="802bc-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="802bc-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="802bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="802bc-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="802bc-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="802bc-118">Scenario description</span></span>
<span data-ttu-id="802bc-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="802bc-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="802bc-121">갤러리에서 Syncplicity 추가</span><span class="sxs-lookup"><span data-stu-id="802bc-121">Adding Syncplicity from the gallery</span></span>
2. <span data-ttu-id="802bc-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="802bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-the-gallery"></a><span data-ttu-id="802bc-123">갤러리에서 Syncplicity 추가</span><span class="sxs-lookup"><span data-stu-id="802bc-123">Adding Syncplicity from the gallery</span></span>
<span data-ttu-id="802bc-124">Syncplicity의 Azure AD 통합을 구성하려면 갤러리의 Syncplicity를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-124">To configure the integration of Syncplicity into Azure AD, you need to add Syncplicity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="802bc-125">**갤러리에서 Syncplicity를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="802bc-125">**To add Syncplicity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="802bc-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="802bc-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="802bc-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="802bc-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="802bc-133">검색 상자에 **Syncplicity**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-133">In the search box, type **Syncplicity**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="802bc-135">결과 창에서 **Syncplicity**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-135">In the results panel, select **Syncplicity**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="802bc-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="802bc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="802bc-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Syncplicity에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="802bc-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Syncplicity 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Syncplicity is to a user in Azure AD.</span></span> <span data-ttu-id="802bc-140">즉, Azure AD 사용자와 Syncplicity의 관련 사용자 간에 연결 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-140">In other words, a link relationship between an Azure AD user and the related user in Syncplicity needs to be established.</span></span>

<span data-ttu-id="802bc-141">Syncplicity에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-141">In Syncplicity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="802bc-142">Syncplicity에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-142">To configure and test Azure AD single sign-on with Syncplicity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="802bc-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="802bc-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="802bc-145">**[Syncplicity 테스트 사용자 만들기](#creating-a-syncplicity-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Syncplicity에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - to have a counterpart of Britta Simon in Syncplicity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="802bc-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="802bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="802bc-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="802bc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="802bc-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Syncplicity 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="802bc-150">**Syncplicity에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="802bc-150">**To configure Azure AD single sign-on with Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="802bc-151">Azure Portal의 **Syncplicity** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-151">In the Azure portal, on the **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="802bc-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="802bc-155">**Syncplicity 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-155">On the **Syncplicity Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="802bc-157">a.</span><span class="sxs-lookup"><span data-stu-id="802bc-157">a.</span></span> <span data-ttu-id="802bc-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="802bc-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="802bc-159">b.</span><span class="sxs-lookup"><span data-stu-id="802bc-159">b.</span></span> <span data-ttu-id="802bc-160">**식별자** 텍스트 상자에서 `https://<companyname>.syncplicity.com/sp` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="802bc-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-161">These values are not real.</span></span> <span data-ttu-id="802bc-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="802bc-163">이러한 값을 얻으려면 [Syncplicity 클라이언트 지원 팀](https://www.syncplicity.com/contact-us)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="802bc-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values.</span></span> 
 

4. <span data-ttu-id="802bc-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="802bc-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="802bc-168">**Syncplicity 구성** 섹션에서 **Syncplicity 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-168">On the **Syncplicity Configuration** section, click **Configure Syncplicity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="802bc-169">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="802bc-171">**Syncplicity** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-171">Sign in to your **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="802bc-172">위쪽에 있는 메뉴에서 **관리자**를 클릭하고 **설정**을 선택한 다음 **사용자 지정 도메인과 Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-172">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="802bc-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="802bc-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="802bc-174">**SSO(Single Sign-On) 설정** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-174">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="802bc-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="802bc-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="802bc-176">a.</span><span class="sxs-lookup"><span data-stu-id="802bc-176">a.</span></span> <span data-ttu-id="802bc-177">**사용자 할당 도메인** 텍스트 상자에 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-177">In the **Custom Domain** textbox, type the name of your domain.</span></span>
  
    <span data-ttu-id="802bc-178">b.</span><span class="sxs-lookup"><span data-stu-id="802bc-178">b.</span></span> <span data-ttu-id="802bc-179">**사용**을 **Single Sign-On 상태**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="802bc-180">c.</span><span class="sxs-lookup"><span data-stu-id="802bc-180">c.</span></span> <span data-ttu-id="802bc-181">Azure Portal에서 복사한 **SAML 엔터티 ID**를 **엔터티 Id** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-181">In the **Entity Id** textbox, Paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="802bc-182">d.</span><span class="sxs-lookup"><span data-stu-id="802bc-182">d.</span></span> <span data-ttu-id="802bc-183">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **로그온 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-183">In the **Sign-in page URL** textbox, Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="802bc-184">e.</span><span class="sxs-lookup"><span data-stu-id="802bc-184">e.</span></span> <span data-ttu-id="802bc-185">Azure Portal에서 복사한 **로그아웃 URL**을 **로그아웃 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-185">In the **Logout page URL** textbox, Paste the **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="802bc-186">f.</span><span class="sxs-lookup"><span data-stu-id="802bc-186">f.</span></span> <span data-ttu-id="802bc-187">**ID 공급자 인증서**에서 **파일 선택**을 클릭하고 Azure Portal에서 다운로드한 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-187">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate which you have downloaded from the Azure portal.</span></span> 

    <span data-ttu-id="802bc-188">g.</span><span class="sxs-lookup"><span data-stu-id="802bc-188">g.</span></span> <span data-ttu-id="802bc-189">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="802bc-190">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="802bc-191">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="802bc-192">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="802bc-193">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="802bc-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="802bc-194">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="802bc-196">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="802bc-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="802bc-197">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="802bc-199">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="802bc-201">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="802bc-203">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="802bc-205">a.</span><span class="sxs-lookup"><span data-stu-id="802bc-205">a.</span></span> <span data-ttu-id="802bc-206">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="802bc-207">b.</span><span class="sxs-lookup"><span data-stu-id="802bc-207">b.</span></span> <span data-ttu-id="802bc-208">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="802bc-209">c.</span><span class="sxs-lookup"><span data-stu-id="802bc-209">c.</span></span> <span data-ttu-id="802bc-210">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="802bc-211">d.</span><span class="sxs-lookup"><span data-stu-id="802bc-211">d.</span></span> <span data-ttu-id="802bc-212">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="802bc-213">Syncplicity 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="802bc-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="802bc-214">AAD 사용자가 로그인할 수 있도록 Syncplicity 응용 프로그램에 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-214">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span></span> <span data-ttu-id="802bc-215">이 섹션은 Syncplicity에 AAD 사용자 계정을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-215">This section describes how to create AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="802bc-216">**사용자 계정을 Syncplicity에 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="802bc-216">**To provision a user account to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="802bc-217">**Syncplicity** 테넌트에 로그인합니다(예: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="802bc-217">Log in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="802bc-218">**관리자**를 클릭하고 **사용자 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="802bc-219">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="802bc-220">![사용자 관리](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="802bc-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="802bc-221">프로비전하려는 AAD 계정의 **이메일 주소**를 입력하고, **사용자**를 **역할**로 선택하고, **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-221">Type the **Email addressess** of an AAD account you want to provision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="802bc-222">![계정 정보](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "계정 정보")</span><span class="sxs-lookup"><span data-stu-id="802bc-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="802bc-223">AAD 계정 소유자가 해당 계정을 확인 및 활성화하기 위한 링크가 포함된 이메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-223">The AAD account holder  gets an email including a link to confirm and activate the account.</span></span> 
    > 

5. <span data-ttu-id="802bc-224">회사에서 새 사용자가 구성원이 되고자 하는 그룹을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="802bc-225">![그룹 멤버 자격](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "그룹 멤버 자격")</span><span class="sxs-lookup"><span data-stu-id="802bc-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="802bc-226">나열된 그룹이 없으면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="802bc-227">사용자의 컴퓨터에서 Syncplicity의 제어 하에 두려는 폴더를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-227">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="802bc-228">![Syncplicity 폴더](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity 폴더")</span><span class="sxs-lookup"><span data-stu-id="802bc-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="802bc-229">다른 Syncplicity 사용자 계정 생성 도구 또는 Syncplicity가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="802bc-230">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="802bc-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="802bc-231">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Syncplicity에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Syncplicity.</span></span>

![사용자 할당][200] 

<span data-ttu-id="802bc-233">**Britta Simon을 Syncplicity에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="802bc-233">**To assign Britta Simon to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="802bc-234">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="802bc-236">응용 프로그램 목록에서 **Syncplicity**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-236">In the applications list, select **Syncplicity**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="802bc-238">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-238">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="802bc-240">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-240">Click **Add** button.</span></span> <span data-ttu-id="802bc-241">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="802bc-243">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="802bc-244">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="802bc-245">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="802bc-246">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="802bc-246">Testing single sign-on</span></span>

<span data-ttu-id="802bc-247">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="802bc-248">액세스 패널에서 Syncplicity 타일을 클릭하면 Syncplicity 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="802bc-248">When you click the Syncplicity tile in the Access Panel, you should get automatically signed-on to your Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="802bc-249">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="802bc-249">Additional resources</span></span>

* [<span data-ttu-id="802bc-250">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="802bc-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="802bc-251">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="802bc-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png


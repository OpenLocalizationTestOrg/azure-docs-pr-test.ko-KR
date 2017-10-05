---
title: "자습서: LockPath Keylight와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 LockPath Keylight 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e64a966f24411818abc4cc4ab29a428b5577d012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="b5f48-103">자습서: Azure Active Directory와 LockPath Keylight 통합</span><span class="sxs-lookup"><span data-stu-id="b5f48-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="b5f48-104">이 자습서에서는 Azure AD(Azure Active Directory)와 LockPath Keylight를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-104">In this tutorial, you learn how to integrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5f48-105">LockPath Keylight를 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-105">Integrating LockPath Keylight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b5f48-106">LockPath Keylight에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-106">You can control in Azure AD who has access to LockPath Keylight</span></span>
- <span data-ttu-id="b5f48-107">사용자가 해당 Azure AD 계정으로 LockPath Keylight에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-107">You can enable your users to automatically get signed-on to LockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b5f48-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b5f48-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5f48-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5f48-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b5f48-110">Prerequisites</span></span>

<span data-ttu-id="b5f48-111">LockPath Keylight와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-111">To configure Azure AD integration with LockPath Keylight, you need the following items:</span></span>

- <span data-ttu-id="b5f48-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b5f48-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5f48-113">LockPath Keylight Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b5f48-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5f48-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5f48-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5f48-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b5f48-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5f48-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5f48-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b5f48-118">Scenario description</span></span>
<span data-ttu-id="b5f48-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5f48-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5f48-121">갤러리에서 LockPath Keylight 추가</span><span class="sxs-lookup"><span data-stu-id="b5f48-121">Adding LockPath Keylight from the gallery</span></span>
2. <span data-ttu-id="b5f48-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b5f48-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-the-gallery"></a><span data-ttu-id="b5f48-123">갤러리에서 LockPath Keylight 추가</span><span class="sxs-lookup"><span data-stu-id="b5f48-123">Adding LockPath Keylight from the gallery</span></span>
<span data-ttu-id="b5f48-124">LockPath Keylight가 Azure AD에 통합되도록 구성하려면 갤러리에서 LockPath Keylight를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-124">To configure the integration of LockPath Keylight into Azure AD, you need to add LockPath Keylight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b5f48-125">**갤러리에서 LockPath Keylight를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5f48-125">**To add LockPath Keylight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b5f48-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5f48-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b5f48-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b5f48-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b5f48-133">검색 상자에 **LockPath Keylight**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-133">In the search box, type **LockPath Keylight**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="b5f48-135">결과 창에서 **LockPath Keylight**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-135">In the results panel, select **LockPath Keylight**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b5f48-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b5f48-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b5f48-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 LockPath Keylight에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b5f48-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 LockPath Keylight 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LockPath Keylight is to a user in Azure AD.</span></span> <span data-ttu-id="b5f48-140">즉, Azure AD 사용자와 LockPath Keylight의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-140">In other words, a link relationship between an Azure AD user and the related user in LockPath Keylight needs to be established.</span></span>

<span data-ttu-id="b5f48-141">LockPath Keylight에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-141">In LockPath Keylight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b5f48-142">LockPath Keylight에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-142">To configure and test Azure AD single sign-on with LockPath Keylight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b5f48-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b5f48-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5f48-145">**[LockPath Keylight 테스트 사용자 만들기](#creating-a-lockpath-keylight-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 LockPath Keylight에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - to have a counterpart of Britta Simon in LockPath Keylight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5f48-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5f48-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b5f48-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b5f48-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b5f48-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 LockPath Keylight 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="b5f48-150">**LockPath Keylight에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5f48-150">**To configure Azure AD single sign-on with LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="b5f48-151">Azure Portal의 **LockPath Keylight** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-151">In the Azure portal, on the **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b5f48-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="b5f48-155">**LockPath Keylight 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-155">On the **LockPath Keylight Domain and URLs** section, perform the following steps::</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="b5f48-157">a.</span><span class="sxs-lookup"><span data-stu-id="b5f48-157">a.</span></span> <span data-ttu-id="b5f48-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="b5f48-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="b5f48-159">b.</span><span class="sxs-lookup"><span data-stu-id="b5f48-159">b.</span></span> <span data-ttu-id="b5f48-160">**식별자** 텍스트 상자에서 `https://<company name>.keylightgrc.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="b5f48-161">c.</span><span class="sxs-lookup"><span data-stu-id="b5f48-161">c.</span></span> <span data-ttu-id="b5f48-162">**회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="b5f48-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b5f48-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-163">These values are not real.</span></span> <span data-ttu-id="b5f48-164">이러한 값을 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b5f48-165">이러한 값을 얻으려면 [LockPath Keylight 클라이언트 지원 팀](https://www.lockpath.com/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="b5f48-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) to get these values.</span></span> 

4. <span data-ttu-id="b5f48-166">**SAML 서명 인증서** 섹션에서 **인증서(원시)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-166">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="b5f48-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="b5f48-170">**LockPath Keylight 구성** 섹션에서 **LockPath Keylight 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-170">On the **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b5f48-171">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="b5f48-173">LockPath Keylight에서 SSO를 사용하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-173">To enable SSO in LockPath Keylight, perform the following steps:</span></span>
   
    <span data-ttu-id="b5f48-174">a.</span><span class="sxs-lookup"><span data-stu-id="b5f48-174">a.</span></span> <span data-ttu-id="b5f48-175">LockPath Keylight 계정에 관리자 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-175">Sign-on to your LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="b5f48-176">b.</span><span class="sxs-lookup"><span data-stu-id="b5f48-176">b.</span></span> <span data-ttu-id="b5f48-177">위쪽 메뉴에서 **사람**을 클릭하고 **Keylight 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-177">In the menu on the top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="b5f48-179">c.</span><span class="sxs-lookup"><span data-stu-id="b5f48-179">c.</span></span> <span data-ttu-id="b5f48-180">왼쪽의 트리 뷰에서 **SAML**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-180">In the treeview on the left, click **SAML**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="b5f48-182">d.</span><span class="sxs-lookup"><span data-stu-id="b5f48-182">d.</span></span> <span data-ttu-id="b5f48-183">**SAML 설정** 대화 상자에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-183">On the **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="b5f48-185">**SAML 설정 편집** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-185">On the **Edit SAML Settings** dialog page, perform the following steps:</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="b5f48-187">a.</span><span class="sxs-lookup"><span data-stu-id="b5f48-187">a.</span></span> <span data-ttu-id="b5f48-188">**SAML 인증**을 **활성**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-188">Set **SAML authentication** to **Active**.</span></span>

    <span data-ttu-id="b5f48-189">b.</span><span class="sxs-lookup"><span data-stu-id="b5f48-189">b.</span></span> <span data-ttu-id="b5f48-190">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **ID 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="b5f48-191">c.</span><span class="sxs-lookup"><span data-stu-id="b5f48-191">c.</span></span> <span data-ttu-id="b5f48-192">Azure Portal에서 복사한 **Single Sign-Out 서비스 URL** 값을 **ID 공급자 로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-192">Paste the **Single Sign-Out Service URL** value which you have copied from the Azure portal into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="b5f48-193">d.</span><span class="sxs-lookup"><span data-stu-id="b5f48-193">d.</span></span> <span data-ttu-id="b5f48-194">**파일 선택**을 클릭하여 다운로드한 LockPath Keylight 인증서를 선택하고 **열기**를 클릭하여 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-194">Click **Choose File** to select your downloaded LockPath Keylight certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="b5f48-195">e.</span><span class="sxs-lookup"><span data-stu-id="b5f48-195">e.</span></span> <span data-ttu-id="b5f48-196">**SAML 사용자 ID 위치**를 **Subject 문의 NameIdentifier 요소**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-196">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span></span>
    
    <span data-ttu-id="b5f48-197">f.</span><span class="sxs-lookup"><span data-stu-id="b5f48-197">f.</span></span> <span data-ttu-id="b5f48-198">**https://&lt;CompanyName&gt;.keylightgrc.com** 패턴을 사용하여 **Keylight 서비스 공급자**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-198">Provide the **Keylight Service Provider** using the following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="b5f48-199">g.</span><span class="sxs-lookup"><span data-stu-id="b5f48-199">g.</span></span> <span data-ttu-id="b5f48-200">**사용자 자동 프로비전**을 **활성**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-200">Set **Auto-provision users** to **Active**.</span></span>

    <span data-ttu-id="b5f48-201">h.</span><span class="sxs-lookup"><span data-stu-id="b5f48-201">h.</span></span> <span data-ttu-id="b5f48-202">**자동 프로비전 계정 유형**을 **전체 사용자**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-202">Set **Auto-provision account type** to **Full User**.</span></span>

    <span data-ttu-id="b5f48-203">i.</span><span class="sxs-lookup"><span data-stu-id="b5f48-203">i.</span></span> <span data-ttu-id="b5f48-204">**Auto-provision security role**(자동 프로비전 보안 역할)에 **Standard User with SAML**(SAML을 사용하는 표준 사용자)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="b5f48-205">j.</span><span class="sxs-lookup"><span data-stu-id="b5f48-205">j.</span></span> <span data-ttu-id="b5f48-206">**Auto-provision security config**(자동 프로비전 보안 구성)에 **Standard User Configuration**(표준 사용자 구성)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="b5f48-207">k.</span><span class="sxs-lookup"><span data-stu-id="b5f48-207">k.</span></span> <span data-ttu-id="b5f48-208">**Email attribute**(이메일 특성) 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-208">In the **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="b5f48-209">l.</span><span class="sxs-lookup"><span data-stu-id="b5f48-209">l.</span></span> <span data-ttu-id="b5f48-210">**First name attribute**(이름 특성) 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-210">In the **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="b5f48-211">m.</span><span class="sxs-lookup"><span data-stu-id="b5f48-211">m.</span></span> <span data-ttu-id="b5f48-212">**Last name attribute**(성 특성) 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-212">In the **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="b5f48-213">n.</span><span class="sxs-lookup"><span data-stu-id="b5f48-213">n.</span></span> <span data-ttu-id="b5f48-214">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b5f48-215">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b5f48-216">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b5f48-217">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b5f48-218">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b5f48-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="b5f48-219">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b5f48-221">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="b5f48-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b5f48-222">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-222">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5f48-224">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-224">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5f48-226">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-226">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5f48-228">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-228">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5f48-230">a.</span><span class="sxs-lookup"><span data-stu-id="b5f48-230">a.</span></span> <span data-ttu-id="b5f48-231">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-231">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5f48-232">b.</span><span class="sxs-lookup"><span data-stu-id="b5f48-232">b.</span></span> <span data-ttu-id="b5f48-233">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-233">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b5f48-234">c.</span><span class="sxs-lookup"><span data-stu-id="b5f48-234">c.</span></span> <span data-ttu-id="b5f48-235">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-235">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b5f48-236">d.</span><span class="sxs-lookup"><span data-stu-id="b5f48-236">d.</span></span> <span data-ttu-id="b5f48-237">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="b5f48-238">LockPath Keylight 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b5f48-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="b5f48-239">이 섹션에서는 LockPath Keylight에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="b5f48-240">LockPath Keylight는 기본적으로 사용하도록 설정된 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="b5f48-241">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-241">There is no action item for you in this section.</span></span> <span data-ttu-id="b5f48-242">사용자가 아직 존재하지 않는 경우 LockPath Keylight에 액세스할 때 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-242">A new user is created when accessing LockPath Keylight if the user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="b5f48-243">사용자를 수동으로 생성해야 하는 경우 [LockPath Keylight 클라이언트 지원 팀](https://www.lockpath.com/contact/)에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-243">If you need to create a user manually, you need to contact the [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b5f48-244">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="b5f48-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b5f48-245">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 LockPath Keylight에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LockPath Keylight.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b5f48-247">**Britta Simon을 LockPath Keylight에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5f48-247">**To assign Britta Simon to LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="b5f48-248">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b5f48-250">응용 프로그램 목록에서 **LockPath Keylight**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-250">In the applications list, select **LockPath Keylight**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="b5f48-252">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-252">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b5f48-254">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-254">Click **Add** button.</span></span> <span data-ttu-id="b5f48-255">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b5f48-257">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b5f48-258">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5f48-259">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b5f48-260">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b5f48-260">Testing single sign-on</span></span>

<span data-ttu-id="b5f48-261">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b5f48-262">액세스 패널에서 LockPath Keylight 타일을 클릭하면 LockPath Keylight 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f48-262">When you click the LockPath Keylight tile in the Access Panel, you should get automatically signed-on to your LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b5f48-263">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b5f48-263">Additional resources</span></span>

* [<span data-ttu-id="b5f48-264">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="b5f48-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5f48-265">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b5f48-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png


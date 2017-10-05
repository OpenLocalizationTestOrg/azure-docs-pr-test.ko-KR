---
title: "자습서: Kudos와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Kudos 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 353798fcfd4ad7ce017fc2fddf4110715db3ace2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="aeb7a-103">자습서: Kudos와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="aeb7a-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="aeb7a-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Kudos를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-104">In this tutorial, you learn how to integrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aeb7a-105">Kudos를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-105">Integrating Kudos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="aeb7a-106">Kudos에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-106">You can control in Azure AD who has access to Kudos</span></span>
- <span data-ttu-id="aeb7a-107">사용자가 해당 Azure AD 계정으로 Kudos에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-107">You can enable your users to automatically get signed-on to Kudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aeb7a-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="aeb7a-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aeb7a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="aeb7a-110">Prerequisites</span></span>

<span data-ttu-id="aeb7a-111">Kudos와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-111">To configure Azure AD integration with Kudos, you need the following items:</span></span>

- <span data-ttu-id="aeb7a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="aeb7a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aeb7a-113">Kudos Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="aeb7a-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aeb7a-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aeb7a-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aeb7a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aeb7a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aeb7a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="aeb7a-118">Scenario description</span></span>
<span data-ttu-id="aeb7a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aeb7a-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aeb7a-121">갤러리에서 Kudos 추가</span><span class="sxs-lookup"><span data-stu-id="aeb7a-121">Adding Kudos from the gallery</span></span>
2. <span data-ttu-id="aeb7a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="aeb7a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-the-gallery"></a><span data-ttu-id="aeb7a-123">갤러리에서 Kudos 추가</span><span class="sxs-lookup"><span data-stu-id="aeb7a-123">Adding Kudos from the gallery</span></span>
<span data-ttu-id="aeb7a-124">Kudos의 Azure AD 통합을 구성하려면 갤러리의 Kudos를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-124">To configure the integration of Kudos into Azure AD, you need to add Kudos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aeb7a-125">**갤러리에서 Kudos를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="aeb7a-125">**To add Kudos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aeb7a-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aeb7a-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="aeb7a-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="aeb7a-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="aeb7a-133">검색 상자에 **Kudos**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-133">In the search box, type **Kudos**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="aeb7a-135">결과 패널에서 **Kudos**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-135">In the results panel, select **Kudos**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aeb7a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="aeb7a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aeb7a-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Kudos에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aeb7a-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Kudos 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kudos is to a user in Azure AD.</span></span> <span data-ttu-id="aeb7a-140">즉, Azure AD 사용자와 Kudos의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-140">In other words, a link relationship between an Azure AD user and the related user in Kudos needs to be established.</span></span>

<span data-ttu-id="aeb7a-141">Kudos에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-141">In Kudos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="aeb7a-142">Kudos에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-142">To configure and test Azure AD single sign-on with Kudos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aeb7a-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aeb7a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aeb7a-145">**[Kudos 테스트 사용자 만들기](#creating-a-kudos-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Kudos에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - to have a counterpart of Britta Simon in Kudos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="aeb7a-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aeb7a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aeb7a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="aeb7a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aeb7a-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Kudos 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="aeb7a-150">**Kudos에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="aeb7a-150">**To configure Azure AD single sign-on with Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="aeb7a-151">Azure Portal의 **Kudos** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-151">In the Azure portal, on the **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="aeb7a-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="aeb7a-155">**Kudos 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-155">On the **Kudos Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="aeb7a-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="aeb7a-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="aeb7a-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-158">This value is not real.</span></span> <span data-ttu-id="aeb7a-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="aeb7a-160">이 값을 얻으려면 [Kudos 클라이언트 지원 팀](http://success.kudosnow.com/home)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) to get this value.</span></span> 
 
4. <span data-ttu-id="aeb7a-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="aeb7a-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aeb7a-165">**Kudos 구성** 섹션에서 **Kudos 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-165">On the **Kudos Configuration** section, click **Configure Kudos** to open **Configure sign-on** window.</span></span> <span data-ttu-id="aeb7a-166">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="aeb7a-168">다른 웹 브라우저 창에서 Kudos 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="aeb7a-169">위쪽의 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-169">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="aeb7a-170">![설정](./media/active-directory-saas-kudos-tutorial/ic787806.png "설정")</span><span class="sxs-lookup"><span data-stu-id="aeb7a-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="aeb7a-171">**통합 \> SSO**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="aeb7a-172">**SSO** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-172">In the **SSO** section, perform the following steps:</span></span>
   
    <span data-ttu-id="aeb7a-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="aeb7a-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="aeb7a-174">a.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-174">a.</span></span> <span data-ttu-id="aeb7a-175">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **로그온 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-175">In **Sign on URL** textbox, paste the value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="aeb7a-176">b.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-176">b.</span></span> <span data-ttu-id="aeb7a-177">Base 64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-177">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="aeb7a-178">c.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-178">c.</span></span> <span data-ttu-id="aeb7a-179">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 URL**에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-179">In **Logout To URL**, paste the value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="aeb7a-180">d.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-180">d.</span></span> <span data-ttu-id="aeb7a-181">**Kudos URL** 텍스트 상자에 회사 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-181">In the **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="aeb7a-182">e.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-182">e.</span></span> <span data-ttu-id="aeb7a-183">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="aeb7a-184">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="aeb7a-185">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="aeb7a-186">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aeb7a-187">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="aeb7a-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="aeb7a-188">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="aeb7a-190">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="aeb7a-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aeb7a-191">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aeb7a-193">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aeb7a-195">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aeb7a-197">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aeb7a-199">a.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-199">a.</span></span> <span data-ttu-id="aeb7a-200">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aeb7a-201">b.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-201">b.</span></span> <span data-ttu-id="aeb7a-202">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aeb7a-203">c.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-203">c.</span></span> <span data-ttu-id="aeb7a-204">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="aeb7a-205">d.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-205">d.</span></span> <span data-ttu-id="aeb7a-206">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="aeb7a-207">Kudos 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="aeb7a-207">Creating a Kudos test user</span></span>

<span data-ttu-id="aeb7a-208">Azure AD 사용자가 Kudos에 로그인할 수 있도록 하려면 Kudos로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-208">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="aeb7a-209">Kudos의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-209">In the case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="aeb7a-210">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="aeb7a-210">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="aeb7a-211">**Kudos** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-211">Log in to your **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="aeb7a-212">위쪽의 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-212">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="aeb7a-213">![설정](./media/active-directory-saas-kudos-tutorial/ic787806.png "설정")</span><span class="sxs-lookup"><span data-stu-id="aeb7a-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="aeb7a-214">**사용자 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="aeb7a-215">**사용자** 탭을 클릭한 다음 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-215">Click the **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="aeb7a-216">![사용자 관리](./media/active-directory-saas-kudos-tutorial/ic787809.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="aeb7a-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="aeb7a-217">**사용자 추가** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-217">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="aeb7a-218">![사용자 추가](./media/active-directory-saas-kudos-tutorial/ic787810.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="aeb7a-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="aeb7a-219">a.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-219">a.</span></span> <span data-ttu-id="aeb7a-220">관련된 텍스트 상자에 프로비전할 유효한 Azure Active Directory 계정의 **이름**, **성**, **전자 메일** 및 기타 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-220">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="aeb7a-221">b.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-221">b.</span></span> <span data-ttu-id="aeb7a-222">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="aeb7a-223">다른 Kudos 사용자 계정 생성 도구 또는 Kudos가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-223">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="aeb7a-224">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="aeb7a-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="aeb7a-225">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Kudos에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kudos.</span></span>

![사용자 할당][200] 

<span data-ttu-id="aeb7a-227">**Britta Simon을 Kudos에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="aeb7a-227">**To assign Britta Simon to Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="aeb7a-228">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="aeb7a-230">응용 프로그램 목록에서 **Kudos**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-230">In the applications list, select **Kudos**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="aeb7a-232">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-232">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="aeb7a-234">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-234">Click **Add** button.</span></span> <span data-ttu-id="aeb7a-235">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="aeb7a-237">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="aeb7a-238">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aeb7a-239">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aeb7a-240">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="aeb7a-240">Testing single sign-on</span></span>

<span data-ttu-id="aeb7a-241">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="aeb7a-242">액세스 패널에서 Kudos 타일을 클릭하면 Kudos 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-242">When you click the Kudos tile in the Access Panel, you should get automatically signed-on to your Kudos application.</span></span> <span data-ttu-id="aeb7a-243">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aeb7a-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aeb7a-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="aeb7a-244">Additional resources</span></span>

* [<span data-ttu-id="aeb7a-245">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="aeb7a-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aeb7a-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="aeb7a-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png


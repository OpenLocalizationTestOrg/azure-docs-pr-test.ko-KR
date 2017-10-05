---
title: "자습서: Sprinklr와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Sprinklr 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 6e1622cd55e3b0e8063604ac9dc0cb0673fa9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="71a08-103">자습서: Sprinklr와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="71a08-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="71a08-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Sprinklr을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-104">In this tutorial, you learn how to integrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71a08-105">Sprinklr을 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-105">Integrating Sprinklr with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="71a08-106">Sprinklr에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-106">You can control in Azure AD who has access to Sprinklr</span></span>
- <span data-ttu-id="71a08-107">사용자가 해당 Azure AD 계정으로 Sprinklr에 자동으로 로그인(Single Sign-On)하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-107">You can enable your users to automatically get signed-on to Sprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="71a08-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="71a08-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71a08-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71a08-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="71a08-110">Prerequisites</span></span>

<span data-ttu-id="71a08-111">Sprinklr과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-111">To configure Azure AD integration with Sprinklr, you need the following items:</span></span>

- <span data-ttu-id="71a08-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="71a08-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71a08-113">Sprinklr Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="71a08-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="71a08-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="71a08-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71a08-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="71a08-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="71a08-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71a08-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="71a08-118">Scenario description</span></span>
<span data-ttu-id="71a08-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71a08-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71a08-121">갤러리에서 Sprinklr 추가</span><span class="sxs-lookup"><span data-stu-id="71a08-121">Adding Sprinklr from the gallery</span></span>
2. <span data-ttu-id="71a08-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="71a08-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-the-gallery"></a><span data-ttu-id="71a08-123">갤러리에서 Sprinklr 추가</span><span class="sxs-lookup"><span data-stu-id="71a08-123">Adding Sprinklr from the gallery</span></span>
<span data-ttu-id="71a08-124">Sprinklr의 Azure AD 통합을 구성하려면 갤러리의 Sprinklr을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-124">To configure the integration of Sprinklr into Azure AD, you need to add Sprinklr from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="71a08-125">**갤러리에서 Sprinklr을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="71a08-125">**To add Sprinklr from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="71a08-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="71a08-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="71a08-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="71a08-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="71a08-133">검색 상자에 **Sprinklr**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-133">In the search box, type **Sprinklr**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="71a08-135">결과 창에서 **Sprinklr**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-135">In the results panel, select **Sprinklr**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="71a08-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="71a08-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="71a08-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Sprinklr에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="71a08-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Sprinklr 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sprinklr is to a user in Azure AD.</span></span> <span data-ttu-id="71a08-140">즉, Azure AD 사용자와 Sprinklr의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-140">In other words, a link relationship between an Azure AD user and the related user in Sprinklr needs to be established.</span></span>

<span data-ttu-id="71a08-141">Sprinklr에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-141">In Sprinklr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="71a08-142">Sprinklr에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-142">To configure and test Azure AD single sign-on with Sprinklr, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="71a08-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="71a08-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="71a08-145">**[Sprinklr 테스트 사용자 만들기](#creating-a-sprinklr-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Sprinklr에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - to have a counterpart of Britta Simon in Sprinklr that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="71a08-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="71a08-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="71a08-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="71a08-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="71a08-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Sprinklr 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="71a08-150">**Sprinklr에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="71a08-150">**To configure Azure AD single sign-on with Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="71a08-151">Azure Portal의 **Sprinklr** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-151">In the Azure portal, on the **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="71a08-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="71a08-155">**Sprinklr 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-155">On the **Sprinklr Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="71a08-157">a.</span><span class="sxs-lookup"><span data-stu-id="71a08-157">a.</span></span> <span data-ttu-id="71a08-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="71a08-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="71a08-159">b.</span><span class="sxs-lookup"><span data-stu-id="71a08-159">b.</span></span> <span data-ttu-id="71a08-160">**식별자** 텍스트 상자에서 `https://<subdomain>.sprinklr.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="71a08-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-161">These values are not real.</span></span> <span data-ttu-id="71a08-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-162">Update the value with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="71a08-163">이러한 값을 얻으려면 [Sprinklr 클라이언트 지원 팀](https://www.sprinklr.com/contact-us/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="71a08-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="71a08-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="71a08-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="71a08-168">**Sprinklr 구성** 섹션에서 **Sprinklr 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-168">On the **Sprinklr Configuration** section, click **Configure Sprinklr** to open **Configure sign-on** window.</span></span> <span data-ttu-id="71a08-169">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

7. <span data-ttu-id="71a08-170">다른 웹 브라우저 창에서 Sprinklr 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-170">In a different web browser window, log in to your Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="71a08-171">**관리 \> 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-171">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="71a08-172">![관리](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "관리")</span><span class="sxs-lookup"><span data-stu-id="71a08-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="71a08-173">왼쪽 창에서 **파트너 관리 \> Single Sign on**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-173">Go to **Manage Partner \> Single Sign** on from the left pane.</span></span>
   
    <span data-ttu-id="71a08-174">![파트너 관리](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "파트너 관리")</span><span class="sxs-lookup"><span data-stu-id="71a08-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="71a08-175">**+Single Sign On 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="71a08-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span><span class="sxs-lookup"><span data-stu-id="71a08-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="71a08-177">**Single Sign on** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-177">On the **Single Sign on** page, perform the following steps:</span></span>
   
    <span data-ttu-id="71a08-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span><span class="sxs-lookup"><span data-stu-id="71a08-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="71a08-179">a.</span><span class="sxs-lookup"><span data-stu-id="71a08-179">a.</span></span> <span data-ttu-id="71a08-180">**이름** 텍스트 상자에 구성의 이름을 입력합니다(예: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="71a08-180">In the **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="71a08-181">b.</span><span class="sxs-lookup"><span data-stu-id="71a08-181">b.</span></span> <span data-ttu-id="71a08-182">**사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-182">Select **Enabled**.</span></span>

    <span data-ttu-id="71a08-183">c.</span><span class="sxs-lookup"><span data-stu-id="71a08-183">c.</span></span> <span data-ttu-id="71a08-184">**새 SSO 인증서 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="71a08-185">e.</span><span class="sxs-lookup"><span data-stu-id="71a08-185">e.</span></span> <span data-ttu-id="71a08-186">Base 64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 **ID 공급자 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-186">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="71a08-187">f.</span><span class="sxs-lookup"><span data-stu-id="71a08-187">f.</span></span> <span data-ttu-id="71a08-188">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **엔터티 Id** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-188">Paste the **SAML Entity ID** value which you have copied from Azure Portal into the **Entity Id** textbox.</span></span>

    <span data-ttu-id="71a08-189">g.</span><span class="sxs-lookup"><span data-stu-id="71a08-189">g.</span></span> <span data-ttu-id="71a08-190">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **ID 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="71a08-191">h.</span><span class="sxs-lookup"><span data-stu-id="71a08-191">h.</span></span> <span data-ttu-id="71a08-192">Azure Portal에서 복사한 **로그아웃 URL** 값을 **ID 공급자 로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-192">Paste the **Sign-Out URL** value which you have copied from Azure Portal into the **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="71a08-193">i.</span><span class="sxs-lookup"><span data-stu-id="71a08-193">i.</span></span> <span data-ttu-id="71a08-194">**SAML 사용자 형식**에서 **어설션에 사용자의 sprinklr.com 사용자 이름 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="71a08-195">j.</span><span class="sxs-lookup"><span data-stu-id="71a08-195">j.</span></span> <span data-ttu-id="71a08-196">**SAML 사용자 ID 위치**로 **Subject 문의 NameIdentifier 요소에 사용자 ID 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-196">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span></span>

    <span data-ttu-id="71a08-197">k.</span><span class="sxs-lookup"><span data-stu-id="71a08-197">k.</span></span> <span data-ttu-id="71a08-198">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-198">Click **Save**.</span></span>
       
    <span data-ttu-id="71a08-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="71a08-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="71a08-200">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="71a08-201">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="71a08-202">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="71a08-203">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="71a08-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="71a08-204">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="71a08-206">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="71a08-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="71a08-207">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="71a08-209">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="71a08-211">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="71a08-213">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="71a08-215">a.</span><span class="sxs-lookup"><span data-stu-id="71a08-215">a.</span></span> <span data-ttu-id="71a08-216">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71a08-217">b.</span><span class="sxs-lookup"><span data-stu-id="71a08-217">b.</span></span> <span data-ttu-id="71a08-218">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="71a08-219">c.</span><span class="sxs-lookup"><span data-stu-id="71a08-219">c.</span></span> <span data-ttu-id="71a08-220">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="71a08-221">d.</span><span class="sxs-lookup"><span data-stu-id="71a08-221">d.</span></span> <span data-ttu-id="71a08-222">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="71a08-223">Sprinklr 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="71a08-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="71a08-224">Sprinklr 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-224">Log in to your Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="71a08-225">**관리 \> 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-225">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="71a08-226">![관리](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "관리")</span><span class="sxs-lookup"><span data-stu-id="71a08-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="71a08-227">왼쪽 창에서 **클라이언트 관리 \> 사용자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-227">Go to **Manage Client \> Users** from the left pane.</span></span>
   
    <span data-ttu-id="71a08-228">![설정](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "설정")</span><span class="sxs-lookup"><span data-stu-id="71a08-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="71a08-229">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="71a08-230">![설정](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "설정")</span><span class="sxs-lookup"><span data-stu-id="71a08-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="71a08-231">**사용자 편집** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-231">On the **Edit user** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="71a08-232">![사용자 편집](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "사용자 편집")</span><span class="sxs-lookup"><span data-stu-id="71a08-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="71a08-233">a.</span><span class="sxs-lookup"><span data-stu-id="71a08-233">a.</span></span> <span data-ttu-id="71a08-234">**메일**, **이름** 및 **성** 텍스트 상자에 프로비전하려는 Azure AD 사용자 계정 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-234">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span></span>

    <span data-ttu-id="71a08-235">b.</span><span class="sxs-lookup"><span data-stu-id="71a08-235">b.</span></span> <span data-ttu-id="71a08-236">**암호 사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="71a08-237">c.</span><span class="sxs-lookup"><span data-stu-id="71a08-237">c.</span></span> <span data-ttu-id="71a08-238">**언어**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-238">Select **Language**.</span></span>

    <span data-ttu-id="71a08-239">d.</span><span class="sxs-lookup"><span data-stu-id="71a08-239">d.</span></span> <span data-ttu-id="71a08-240">**사용자 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-240">Select **User Type**.</span></span>

    <span data-ttu-id="71a08-241">e.</span><span class="sxs-lookup"><span data-stu-id="71a08-241">e.</span></span> <span data-ttu-id="71a08-242">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="71a08-243">**암호 사용 안 함** 을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-243">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="71a08-244">**역할**로 이동하고 다음 단계를 수행하십시오.</span><span class="sxs-lookup"><span data-stu-id="71a08-244">Go to **Role**, and then perform the following steps:</span></span>
   
    <span data-ttu-id="71a08-245">![파트너 역할](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "파트너 역할")</span><span class="sxs-lookup"><span data-stu-id="71a08-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="71a08-246">a.</span><span class="sxs-lookup"><span data-stu-id="71a08-246">a.</span></span> <span data-ttu-id="71a08-247">**전역** 목록에서 **ALL\_Permissions**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-247">From the **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="71a08-248">b.</span><span class="sxs-lookup"><span data-stu-id="71a08-248">b.</span></span> <span data-ttu-id="71a08-249">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="71a08-250">다른 Sprinklr 사용자 계정 생성 도구 또는 Sprinklr가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="71a08-251">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="71a08-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="71a08-252">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Sprinklr에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sprinklr.</span></span>

![사용자 할당][200] 

<span data-ttu-id="71a08-254">**Britta Simon을 Sprinklr에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="71a08-254">**To assign Britta Simon to Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="71a08-255">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="71a08-257">응용 프로그램 목록에서 **Sprinklr**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-257">In the applications list, select **Sprinklr**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="71a08-259">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-259">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="71a08-261">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-261">Click **Add** button.</span></span> <span data-ttu-id="71a08-262">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="71a08-264">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="71a08-265">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="71a08-266">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="71a08-267">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="71a08-267">Testing single sign-on</span></span>

<span data-ttu-id="71a08-268">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="71a08-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="71a08-269">액세스 패널에서 Sprinklr 타일을 클릭하면 Sprinklr 응용 프로그램에 자동으로 로그인됩니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71a08-269">When you click the Sprinklr tile in the Access Panel, you should get automatically signed-on to your Sprinklr application For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="71a08-270">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="71a08-270">Additional resources</span></span>

* [<span data-ttu-id="71a08-271">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="71a08-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71a08-272">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="71a08-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png


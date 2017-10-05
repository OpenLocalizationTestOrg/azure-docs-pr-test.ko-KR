---
title: "자습서: Namely와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Namely 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 1d7e8fbcfc757853ab909bbb05522f3dc387715d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="78be8-103">자습서: Namely와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="78be8-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="78be8-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Mozy Enterprise를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-104">In this tutorial, you learn how to integrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78be8-105">Namely를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-105">Integrating Namely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="78be8-106">Namely에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-106">You can control in Azure AD who has access to Namely</span></span>
- <span data-ttu-id="78be8-107">사용자가 해당 Azure AD 계정으로 Namely에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-107">You can enable your users to automatically get signed-on to Namely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78be8-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="78be8-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78be8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78be8-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="78be8-110">Prerequisites</span></span>

<span data-ttu-id="78be8-111">Namely와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-111">To configure Azure AD integration with Namely, you need the following items:</span></span>

- <span data-ttu-id="78be8-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="78be8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78be8-113">Namely Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="78be8-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78be8-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78be8-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78be8-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="78be8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78be8-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78be8-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="78be8-118">Scenario description</span></span>
<span data-ttu-id="78be8-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78be8-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78be8-121">갤러리에서 Namely 추가</span><span class="sxs-lookup"><span data-stu-id="78be8-121">Adding Namely from the gallery</span></span>
2. <span data-ttu-id="78be8-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="78be8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-the-gallery"></a><span data-ttu-id="78be8-123">갤러리에서 Namely 추가</span><span class="sxs-lookup"><span data-stu-id="78be8-123">Adding Namely from the gallery</span></span>
<span data-ttu-id="78be8-124">Namely의 Azure AD 통합을 구성하려면 갤러리의 Namely를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-124">To configure the integration of Namely into Azure AD, you need to add Namely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="78be8-125">**갤러리에서 Namely를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="78be8-125">**To add Namely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="78be8-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="78be8-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="78be8-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="78be8-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="78be8-133">검색 상자에서 **Namely**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-133">In the search box, type **Namely**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="78be8-135">결과 패널에서 **Namely**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-135">In the results panel, select **Namely**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78be8-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="78be8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78be8-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Namely에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="78be8-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Namely 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Namely is to a user in Azure AD.</span></span> <span data-ttu-id="78be8-140">즉, Azure AD 사용자와 Namely의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-140">In other words, a link relationship between an Azure AD user and the related user in Namely needs to be established.</span></span>

<span data-ttu-id="78be8-141">Namely에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-141">In Namely, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="78be8-142">Namely에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-142">To configure and test Azure AD single sign-on with Namely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="78be8-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="78be8-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78be8-145">**[Namely 테스트 사용자 만들기](#creating-a-namely-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Namely에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - to have a counterpart of Britta Simon in Namely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="78be8-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78be8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78be8-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="78be8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78be8-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Namely 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="78be8-150">**Namely에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="78be8-150">**To configure Azure AD single sign-on with Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="78be8-151">Azure Portal의 **Namely** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-151">In the Azure portal, on the **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="78be8-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="78be8-155">**Namely 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-155">On the **Namely Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="78be8-157">a.</span><span class="sxs-lookup"><span data-stu-id="78be8-157">a.</span></span> <span data-ttu-id="78be8-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="78be8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="78be8-159">b.</span><span class="sxs-lookup"><span data-stu-id="78be8-159">b.</span></span> <span data-ttu-id="78be8-160">**식별자** 텍스트 상자에서 `https://<subdomain>.namely.com/saml/metadata` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="78be8-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-161">These values are not real.</span></span> <span data-ttu-id="78be8-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="78be8-163">이러한 값을 얻으려면 [Namely 클라이언트 지원 팀](https://www.namely.com/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="78be8-163">Contact [Namely Client support team](https://www.namely.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="78be8-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="78be8-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78be8-168">**Namely 구성** 섹션에서 **Namely 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-168">On the **Namely Configuration** section, click **Configure Namely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="78be8-169">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="78be8-171">다른 웹 브라우저 창에서 Namely 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-171">In another browser window, sign on to your Namely company site as an administrator.</span></span>

8. <span data-ttu-id="78be8-172">위쪽 도구 모음에서 **회사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-172">In the toolbar on the top, click **Company**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="78be8-174">**설정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-174">Click the **Settings** tab.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="78be8-176">**SAML**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-176">Click **SAML**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="78be8-178">**SAML 설정** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-178">On the **SAML Settings** page, perform the following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="78be8-180">a.</span><span class="sxs-lookup"><span data-stu-id="78be8-180">a.</span></span> <span data-ttu-id="78be8-181">**SAML 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="78be8-182">b.</span><span class="sxs-lookup"><span data-stu-id="78be8-182">b.</span></span> <span data-ttu-id="78be8-183">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **ID 공급자 SSO URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-183">In the **Identity provider SSO url** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="78be8-184">c.</span><span class="sxs-lookup"><span data-stu-id="78be8-184">c.</span></span> <span data-ttu-id="78be8-185">다운로드된 인증서를 메모장에서 열고 내용을 복사한 다음 전체 인증서를 **ID 공급자 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-185">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="78be8-186">d.</span><span class="sxs-lookup"><span data-stu-id="78be8-186">d.</span></span> <span data-ttu-id="78be8-187">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="78be8-188">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="78be8-189">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="78be8-190">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78be8-191">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="78be8-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="78be8-192">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="78be8-194">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="78be8-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="78be8-195">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78be8-197">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78be8-199">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78be8-201">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78be8-203">a.</span><span class="sxs-lookup"><span data-stu-id="78be8-203">a.</span></span> <span data-ttu-id="78be8-204">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78be8-205">b.</span><span class="sxs-lookup"><span data-stu-id="78be8-205">b.</span></span> <span data-ttu-id="78be8-206">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78be8-207">c.</span><span class="sxs-lookup"><span data-stu-id="78be8-207">c.</span></span> <span data-ttu-id="78be8-208">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="78be8-209">d.</span><span class="sxs-lookup"><span data-stu-id="78be8-209">d.</span></span> <span data-ttu-id="78be8-210">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="78be8-211">Namely 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="78be8-211">Creating a Namely test user</span></span>

<span data-ttu-id="78be8-212">이 섹션은 Namely에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-212">The objective of this section is to create a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="78be8-213">**Namely에서 Britta Simon이라는 사용자를 만들려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="78be8-213">**To create a user called Britta Simon in Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="78be8-214">Namely 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-214">Sign-on to your Namely company site as an administrator.</span></span>

2. <span data-ttu-id="78be8-215">위쪽 도구 모음에서 **사람**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-215">In the toolbar on the top, click **People**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="78be8-217">**디렉터리** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-217">Click the **Directory** tab.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="78be8-219">**새 사람 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-219">Click **Add New Person**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="78be8-221">**새 사람 추가** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-221">On the **Add New Person** dialog, perform the following steps:</span></span>

    <span data-ttu-id="78be8-222">a.</span><span class="sxs-lookup"><span data-stu-id="78be8-222">a.</span></span> <span data-ttu-id="78be8-223">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-223">In the **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="78be8-224">b.</span><span class="sxs-lookup"><span data-stu-id="78be8-224">b.</span></span> <span data-ttu-id="78be8-225">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-225">In the **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="78be8-226">c.</span><span class="sxs-lookup"><span data-stu-id="78be8-226">c.</span></span> <span data-ttu-id="78be8-227">**메일** 텍스트 상자에 BrittaSimon의 **메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-227">In the **Email** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78be8-228">d.</span><span class="sxs-lookup"><span data-stu-id="78be8-228">d.</span></span> <span data-ttu-id="78be8-229">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-229">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="78be8-230">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="78be8-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="78be8-231">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Namely에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Namely.</span></span>

![사용자 할당][200] 

<span data-ttu-id="78be8-233">**Britta Simon을 Namely에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="78be8-233">**To assign Britta Simon to Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="78be8-234">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="78be8-236">응용 프로그램 목록에서 **Namely**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-236">In the applications list, select **Namely**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="78be8-238">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-238">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="78be8-240">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-240">Click **Add** button.</span></span> <span data-ttu-id="78be8-241">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="78be8-243">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="78be8-244">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78be8-245">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78be8-246">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="78be8-246">Testing single sign-on</span></span>

<span data-ttu-id="78be8-247">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-247">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="78be8-248">액세스 패널에서 Namely 타일을 클릭하면 Namely 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="78be8-248">When you click the Namely tile in the Access Panel, you should get automatically signed-on to your Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78be8-249">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="78be8-249">Additional resources</span></span>

* [<span data-ttu-id="78be8-250">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="78be8-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78be8-251">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="78be8-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png


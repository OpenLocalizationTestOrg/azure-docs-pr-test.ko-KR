---
title: "자습서: Recognize와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Recognize 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 97d85183d0307c41a3b879d440d87a6fb0c53190
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="a30f2-103">자습서: Recognize와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a30f2-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="a30f2-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Recognize를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-104">In this tutorial, you learn how to integrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a30f2-105">Recognize를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-105">Integrating Recognize with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a30f2-106">Recognize에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-106">You can control in Azure AD who has access to Recognize</span></span>
- <span data-ttu-id="a30f2-107">사용자가 해당 Azure AD 계정으로 Recognize에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-107">You can enable your users to automatically get signed-on to Recognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a30f2-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a30f2-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a30f2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a30f2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a30f2-110">Prerequisites</span></span>

<span data-ttu-id="a30f2-111">Recognize와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-111">To configure Azure AD integration with Recognize, you need the following items:</span></span>

- <span data-ttu-id="a30f2-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a30f2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a30f2-113">Recognize Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a30f2-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a30f2-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a30f2-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a30f2-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a30f2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a30f2-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a30f2-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a30f2-118">Scenario description</span></span>
<span data-ttu-id="a30f2-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a30f2-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a30f2-121">갤러리에서 Recognize 추가</span><span class="sxs-lookup"><span data-stu-id="a30f2-121">Adding Recognize from the gallery</span></span>
2. <span data-ttu-id="a30f2-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a30f2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-the-gallery"></a><span data-ttu-id="a30f2-123">갤러리에서 Recognize 추가</span><span class="sxs-lookup"><span data-stu-id="a30f2-123">Adding Recognize from the gallery</span></span>
<span data-ttu-id="a30f2-124">Recognize의 Azure AD 통합을 구성하려면 갤러리의 Recognize를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a30f2-125">**갤러리에서 Recognize를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a30f2-125">**To add Recognize from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a30f2-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a30f2-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a30f2-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a30f2-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a30f2-133">검색 상자에 **Recognize**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-133">In the search box, type **Recognize**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="a30f2-135">결과 패널에서 **Recognize**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-135">In the results panel, select **Recognize**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a30f2-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a30f2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a30f2-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Recognize에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a30f2-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Recognize 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Recognize is to a user in Azure AD.</span></span> <span data-ttu-id="a30f2-140">즉, Azure AD 사용자와 Recognize의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-140">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span></span>

<span data-ttu-id="a30f2-141">Recognize에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-141">In Recognize, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a30f2-142">Recognize에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-142">To configure and test Azure AD single sign-on with Recognize, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a30f2-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a30f2-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a30f2-145">**[Recognize 테스트 사용자 만들기](#creating-a-recognize-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Recognize에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a30f2-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a30f2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a30f2-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a30f2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a30f2-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Recognize 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="a30f2-150">**Recognize에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a30f2-150">**To configure Azure AD single sign-on with Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="a30f2-151">Azure Portal의 **Recognize** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-151">In the Azure portal, on the **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a30f2-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="a30f2-155">**Recognize 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-155">On the **Recognize Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="a30f2-157">a.</span><span class="sxs-lookup"><span data-stu-id="a30f2-157">a.</span></span> <span data-ttu-id="a30f2-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="a30f2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="a30f2-159">b.</span><span class="sxs-lookup"><span data-stu-id="a30f2-159">b.</span></span> <span data-ttu-id="a30f2-160">**식별자** 텍스트 상자에서 `https://recognizeapp.com/<your-domain>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a30f2-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-161">These values are not real.</span></span> <span data-ttu-id="a30f2-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a30f2-163">[Recognize 클라이언트 지원 팀](mailto:support@recognizeapp.com)에 문의하여 로그온 URL을 얻고 자습서 뒷부분에 설명된 [SSO Settings](SSO 설정) 섹션에서 [Service Provider Metadata URL](서비스 공급자 메타데이터 URL)을 열러 식별자 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening the Service Provider Metadata URL from the SSO Settings section that is explained later in the tutorial.</span></span> <span data-ttu-id="a30f2-164">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a30f2-164">.</span></span> 
 
4. <span data-ttu-id="a30f2-165">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="a30f2-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-167">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a30f2-169">**Recognize 구성** 섹션에서 **Recognize 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-169">On the **Recognize Configuration** section, click **Configure Recognize** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a30f2-170">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="a30f2-172">다른 웹 브라우저 창에서 Recognize 테넌트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-172">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="a30f2-173">오른쪽 위 모서리에서 **메뉴**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-173">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="a30f2-174">**회사 관리자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-174">Go to **Company Admin**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="a30f2-176">왼쪽 탐색 창에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-176">On the left navigation pane, click **Settings**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="a30f2-178">**SSO 설정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-178">Perform the following steps on **SSO Settings** section.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="a30f2-180">a.</span><span class="sxs-lookup"><span data-stu-id="a30f2-180">a.</span></span> <span data-ttu-id="a30f2-181">**SSO 사용**에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="a30f2-182">b.</span><span class="sxs-lookup"><span data-stu-id="a30f2-182">b.</span></span> <span data-ttu-id="a30f2-183">Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **IDP 엔터티 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a30f2-184">c.</span><span class="sxs-lookup"><span data-stu-id="a30f2-184">c.</span></span> <span data-ttu-id="a30f2-185">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **Sso target url**(SSO 대상 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-185">In the **Sso target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a30f2-186">d.</span><span class="sxs-lookup"><span data-stu-id="a30f2-186">d.</span></span> <span data-ttu-id="a30f2-187">Azure Portal에서 복사한 **로그아웃 URL** 값을 **Slo target url**(SLO 대상 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-187">In the **Slo target url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="a30f2-188">e.</span><span class="sxs-lookup"><span data-stu-id="a30f2-188">e.</span></span> <span data-ttu-id="a30f2-189">다운로드한 **인증서(Base64)** 파일을 메모장에서 열고 내용을 클립보드에 복사한 다음 **인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-189">Open your downloaded **Certificate (Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="a30f2-190">f.</span><span class="sxs-lookup"><span data-stu-id="a30f2-190">f.</span></span> <span data-ttu-id="a30f2-191">**설정 저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-191">Click the **Save settings** button.</span></span> 

11. <span data-ttu-id="a30f2-192">**SSO 설정** 섹션 옆의 **서비스 공급자 메타데이터 URL**에서 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-192">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="a30f2-194">빈 브라우저에서 **메타데이터 URL 링크**를 열어서 메타데이터 문서를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-194">Open the **Metadata URL link** under a blank browser to download the metadata document.</span></span> <span data-ttu-id="a30f2-195">그런 다음 파일에서 EntityDescriptor 값(entityID)을 복사하여 Azure Portal **Recognize 도메인 및 URL** 섹션의 **식별자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-195">Then copy the EntityDescriptor value(entityID) from the file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="a30f2-197">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a30f2-198">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a30f2-199">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a30f2-200">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a30f2-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="a30f2-201">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a30f2-203">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="a30f2-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a30f2-204">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a30f2-206">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a30f2-208">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a30f2-210">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a30f2-212">a.</span><span class="sxs-lookup"><span data-stu-id="a30f2-212">a.</span></span> <span data-ttu-id="a30f2-213">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a30f2-214">b.</span><span class="sxs-lookup"><span data-stu-id="a30f2-214">b.</span></span> <span data-ttu-id="a30f2-215">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a30f2-216">c.</span><span class="sxs-lookup"><span data-stu-id="a30f2-216">c.</span></span> <span data-ttu-id="a30f2-217">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a30f2-218">d.</span><span class="sxs-lookup"><span data-stu-id="a30f2-218">d.</span></span> <span data-ttu-id="a30f2-219">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="a30f2-220">Recognize 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a30f2-220">Creating a Recognize test user</span></span>

<span data-ttu-id="a30f2-221">Azure AD 사용자가 Recognize에 로그인할 수 있도록 하려면 Recognize로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-221">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="a30f2-222">Recognize의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-222">In the case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="a30f2-223">이 앱은 SCIM 프로비전을 지원하지 않지만 사용자를 프로비전하는 대체 사용자 동기화 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="a30f2-224">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a30f2-224">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a30f2-225">Recognize 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="a30f2-226">오른쪽 위 모서리에서 **메뉴**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-226">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="a30f2-227">**회사 관리자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-227">Go to **Company Admin**.</span></span>

3. <span data-ttu-id="a30f2-228">왼쪽 탐색 창에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-228">On the left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="a30f2-229">**사용자 동기화** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-229">Perform the following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="a30f2-230">![새 사용자](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="a30f2-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="a30f2-231">a.</span><span class="sxs-lookup"><span data-stu-id="a30f2-231">a.</span></span> <span data-ttu-id="a30f2-232">**동기화 사용**에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="a30f2-233">b.</span><span class="sxs-lookup"><span data-stu-id="a30f2-233">b.</span></span> <span data-ttu-id="a30f2-234">**동기화 공급자 선택**에서 **Microsoft/Office 365**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="a30f2-235">c.</span><span class="sxs-lookup"><span data-stu-id="a30f2-235">c.</span></span> <span data-ttu-id="a30f2-236">**사용자 동기화 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-236">Click **Run User Sync**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a30f2-237">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a30f2-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a30f2-238">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Recognize에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Recognize.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a30f2-240">**Britta Simon을 Recognize에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="a30f2-240">**To assign Britta Simon to Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="a30f2-241">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a30f2-243">응용 프로그램 목록에서 **Recognize**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-243">In the applications list, select **Recognize**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="a30f2-245">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-245">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a30f2-247">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-247">Click **Add** button.</span></span> <span data-ttu-id="a30f2-248">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a30f2-250">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a30f2-251">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a30f2-252">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a30f2-253">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a30f2-253">Testing single sign-on</span></span>

<span data-ttu-id="a30f2-254">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a30f2-255">액세스 패널에서 Recognize 타일을 클릭하면 Recognize 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="a30f2-255">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span></span> <span data-ttu-id="a30f2-256">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a30f2-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a30f2-257">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a30f2-257">Additional resources</span></span>

* [<span data-ttu-id="a30f2-258">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="a30f2-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a30f2-259">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a30f2-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png


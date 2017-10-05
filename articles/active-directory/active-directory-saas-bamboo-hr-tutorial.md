---
title: "자습서: Azure Active Directory와 BambooHR 통합| Microsoft Docs"
description: "Azure Active Directory 및 BambooHR 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: 06bf91b0e598fd3d8e644378efdb753611ee1ebc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="96d12-103">자습서: BambooHR과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="96d12-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="96d12-104">이 자습서에서는 Azure AD(Azure Active Directory)와 BambooHR을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-104">In this tutorial, you learn how to integrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96d12-105">BambooHR을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-105">Integrating BambooHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="96d12-106">BambooHR에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-106">You can control in Azure AD who has access to BambooHR</span></span>
- <span data-ttu-id="96d12-107">사용자가 해당 Azure AD 계정으로 BambooHR에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-107">You can enable your users to automatically get signed-on to BambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96d12-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="96d12-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96d12-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96d12-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="96d12-110">Prerequisites</span></span>

<span data-ttu-id="96d12-111">BambooHR과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-111">To configure Azure AD integration with BambooHR, you need the following items:</span></span>

- <span data-ttu-id="96d12-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="96d12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96d12-113">BambooHR Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="96d12-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96d12-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96d12-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96d12-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="96d12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96d12-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96d12-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="96d12-118">Scenario description</span></span>
<span data-ttu-id="96d12-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96d12-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96d12-121">갤러리에서 BambooHR 추가</span><span class="sxs-lookup"><span data-stu-id="96d12-121">Adding BambooHR from the gallery</span></span>
2. <span data-ttu-id="96d12-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="96d12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-the-gallery"></a><span data-ttu-id="96d12-123">갤러리에서 BambooHR 추가</span><span class="sxs-lookup"><span data-stu-id="96d12-123">Adding BambooHR from the gallery</span></span>
<span data-ttu-id="96d12-124">BambooHR의 Azure AD 통합을 구성하려면 갤러리의 BambooHR을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-124">To configure the integration of BambooHR into Azure AD, you need to add BambooHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="96d12-125">**갤러리에서 BambooHR을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="96d12-125">**To add BambooHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="96d12-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="96d12-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="96d12-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="96d12-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="96d12-133">검색 상자에 **BambooHR**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-133">In the search box, type **BambooHR**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="96d12-135">결과 패널에서 **BambooHR**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-135">In the results panel, select **BambooHR**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96d12-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="96d12-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96d12-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 BambooHR에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="96d12-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 BambooHR 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BambooHR is to a user in Azure AD.</span></span> <span data-ttu-id="96d12-140">즉, Azure AD 사용자와 BambooHR의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-140">In other words, a link relationship between an Azure AD user and the related user in BambooHR needs to be established.</span></span>

<span data-ttu-id="96d12-141">BambooHR에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-141">In BambooHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="96d12-142">BambooHR에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-142">To configure and test Azure AD single sign-on with BambooHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="96d12-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="96d12-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96d12-145">**[BambooHR 테스트 사용자 만들기](#creating-a-bamboohr-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 해당 사용자를 BambooHR에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - to have a counterpart of Britta Simon in BambooHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="96d12-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96d12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96d12-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="96d12-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96d12-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 BambooHR 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="96d12-150">**BambooHR에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="96d12-150">**To configure Azure AD single sign-on with BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="96d12-151">Azure Portal의 **BambooHR** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-151">In the Azure portal, on the **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="96d12-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="96d12-155">**BambooHR 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-155">On the **BambooHR Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="96d12-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="96d12-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="96d12-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-158">This value is not real.</span></span> <span data-ttu-id="96d12-159">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="96d12-160">이 값을 얻으려면 [BambooHR 클라이언트 지원팀](https://www.bamboohr.com/contact.php)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="96d12-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) to get this value.</span></span> 
 
4. <span data-ttu-id="96d12-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="96d12-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="96d12-165">**BambooHR 구성** 섹션에서 **BambooHR 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-165">On the **BambooHR Configuration** section, click **Configure BambooHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="96d12-166">**빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="96d12-168">다른 웹 브라우저 창에서 BambooHR 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="96d12-169">홈페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-169">On the homepage, perform the following steps:</span></span>
   
    <span data-ttu-id="96d12-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96d12-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="96d12-171">a.</span><span class="sxs-lookup"><span data-stu-id="96d12-171">a.</span></span> <span data-ttu-id="96d12-172">**앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="96d12-173">b.</span><span class="sxs-lookup"><span data-stu-id="96d12-173">b.</span></span> <span data-ttu-id="96d12-174">왼쪽의 앱 메뉴에서 **Single Sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-174">In the apps menu on the left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="96d12-175">c.</span><span class="sxs-lookup"><span data-stu-id="96d12-175">c.</span></span> <span data-ttu-id="96d12-176">**SAML Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="96d12-177">**SAML Single Sign-On** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-177">In the **SAML Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="96d12-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="96d12-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="96d12-179">a.</span><span class="sxs-lookup"><span data-stu-id="96d12-179">a.</span></span> <span data-ttu-id="96d12-180">**SAML Single Sign-On 서비스 URL** 값을 **SSO 로그인 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-180">Paste the **SAML Single Sign-On Service URL** value into the **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="96d12-181">b.</span><span class="sxs-lookup"><span data-stu-id="96d12-181">b.</span></span> <span data-ttu-id="96d12-182">Azure Portal에서 다운로드한 Base-64로 인코딩된 인증서를 메모장에서 열고, 콘텐츠를 클립보드에 복사한 다음, **X.509 인증서** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="96d12-183">c.</span><span class="sxs-lookup"><span data-stu-id="96d12-183">c.</span></span> <span data-ttu-id="96d12-184">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="96d12-185">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="96d12-186">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="96d12-187">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96d12-188">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="96d12-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="96d12-189">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="96d12-191">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="96d12-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="96d12-192">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96d12-194">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96d12-196">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96d12-198">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96d12-200">a.</span><span class="sxs-lookup"><span data-stu-id="96d12-200">a.</span></span> <span data-ttu-id="96d12-201">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96d12-202">b.</span><span class="sxs-lookup"><span data-stu-id="96d12-202">b.</span></span> <span data-ttu-id="96d12-203">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96d12-204">c.</span><span class="sxs-lookup"><span data-stu-id="96d12-204">c.</span></span> <span data-ttu-id="96d12-205">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="96d12-206">d.</span><span class="sxs-lookup"><span data-stu-id="96d12-206">d.</span></span> <span data-ttu-id="96d12-207">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="96d12-208">BambooHR 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="96d12-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="96d12-209">Azure AD 사용자가 BambooHR에 로그인할 수 있도록 하려면 BambooHR로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-209">To enable Azure AD users to log in to BambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="96d12-210">BambooHR의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-210">In the case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="96d12-211">**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="96d12-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="96d12-212">**BambooHR** 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-212">Log in to your **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="96d12-213">위쪽에 도구 모음에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-213">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="96d12-214">![설정](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "설정")</span><span class="sxs-lookup"><span data-stu-id="96d12-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="96d12-215">**개요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-215">Click **Overview**.</span></span>

4. <span data-ttu-id="96d12-216">왼쪽 탐색 창에서 **보안 \> 사용자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-216">In the left navigation pane, go to **Security \> Users**.</span></span>

5. <span data-ttu-id="96d12-217">관련된 텍스트 상자에 프로비전할 유효한 AAD 계정의 사용자 이름, 암호 및 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-217">Type the user name, password, and email address of a valid AAD account you want to provision into the related textboxes.</span></span>

6. <span data-ttu-id="96d12-218">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="96d12-219">다른 BambooHR 사용자 계정 생성 도구 또는 BambooHR이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="96d12-220">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="96d12-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="96d12-221">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 BambooHR에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BambooHR.</span></span>

![사용자 할당][200] 

<span data-ttu-id="96d12-223">**Britta Simon을 BambooHR에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="96d12-223">**To assign Britta Simon to BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="96d12-224">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="96d12-226">응용 프로그램 목록에서 **BambooHR**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-226">In the applications list, select **BambooHR**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="96d12-228">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-228">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="96d12-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-230">Click **Add** button.</span></span> <span data-ttu-id="96d12-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="96d12-233">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="96d12-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96d12-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="96d12-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="96d12-236">Testing single sign-on</span></span>

<span data-ttu-id="96d12-237">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="96d12-238">액세스 패널에서 BambooHR 타일을 클릭하면 BambooHR 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="96d12-238">When you click the BambooHR tile in the Access Panel, you should get automatically signed-on to your BambooHR application.</span></span>
<span data-ttu-id="96d12-239">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96d12-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="96d12-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="96d12-240">Additional resources</span></span>

* [<span data-ttu-id="96d12-241">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="96d12-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96d12-242">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="96d12-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png


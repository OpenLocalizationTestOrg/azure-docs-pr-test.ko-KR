---
title: "자습서: Jobscience와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Jobscience 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 66bec35a8f17482433dbf02827b90620d1cff378
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="b918c-103">자습서: Jobscience와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b918c-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="b918c-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Jobscience를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b918c-105">Jobscience를 Azure AD와 통합하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b918c-106">Jobscience에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-106">You can control in Azure AD who has access to Jobscience</span></span>
- <span data-ttu-id="b918c-107">사용자가 자신의 Azure AD 계정으로 Jobscience에 자동으로 로그온(Single Sign-On) 되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b918c-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b918c-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b918c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b918c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b918c-110">Prerequisites</span></span>

<span data-ttu-id="b918c-111">Jobscience와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-111">To configure Azure AD integration with Jobscience, you need the following items:</span></span>

- <span data-ttu-id="b918c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b918c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b918c-113">Jobscience Single Sign-On이 가능하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b918c-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b918c-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b918c-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b918c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b918c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b918c-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b918c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b918c-118">Scenario description</span></span>
<span data-ttu-id="b918c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b918c-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b918c-121">갤러리에서 Jobscience 추가</span><span class="sxs-lookup"><span data-stu-id="b918c-121">Adding Jobscience from the gallery</span></span>
2. <span data-ttu-id="b918c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b918c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-the-gallery"></a><span data-ttu-id="b918c-123">갤러리에서 Jobscience 추가</span><span class="sxs-lookup"><span data-stu-id="b918c-123">Adding Jobscience from the gallery</span></span>
<span data-ttu-id="b918c-124">Jobscience가 Azure AD에 통합되도록 구성하려면 갤러리에서 Jobscience를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b918c-125">**갤러리에서 Jobscience를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b918c-125">**To add Jobscience from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b918c-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b918c-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b918c-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b918c-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b918c-133">검색 상자에 **Jobscience**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-133">In the search box, type **Jobscience**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="b918c-135">결과 창에서 **Jobscience**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b918c-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b918c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b918c-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Jobscience에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b918c-139">Single Sign-On이 작동하려면 Azure AD 사용자에 해당하는 Jobscience 사용자가 누구인지 Azure AD에서 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span></span> <span data-ttu-id="b918c-140">즉, Azure AD 사용자와 Jobscience의 관련 사용자 간에 링크 관계가 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span></span>

<span data-ttu-id="b918c-141">Jobscience에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b918c-142">Jobscience에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b918c-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b918c-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b918c-145">**[Jobscience 테스트 사용자 만들기](#creating-a-jobscience-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Jobscience에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b918c-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b918c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b918c-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b918c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b918c-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Jobscience 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="b918c-150">**Jobscience에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b918c-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="b918c-151">Azure Portal의 **Jobscience** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b918c-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="b918c-155">**Jobscience 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="b918c-157">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="b918c-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b918c-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-158">This value is not real.</span></span> <span data-ttu-id="b918c-159">실제 로그온 URL로 이 값을 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="b918c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b918c-160">이 값은 [Jobscience 클라이언트 지원 팀](https://www.jobscience.com/support) 또는 앞으로 만들 SSO 프로필에서 참조하세요. 이 내용은 자습서의 뒷부분에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span></span> 
 
4. <span data-ttu-id="b918c-161">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="b918c-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b918c-165">**Jobscience 구성** 섹션에서 **Jobscience 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b918c-166">**빠른 참조 섹션**에서 **로그아웃 URL, SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="b918c-168">Jobscience 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-168">Log in to your Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="b918c-169">**설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-169">Go to **Setup**.</span></span>
   
   <span data-ttu-id="b918c-170">![설치](./media/active-directory-saas-jobscience-tutorial/IC784358.png "설치")</span><span class="sxs-lookup"><span data-stu-id="b918c-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="b918c-171">왼쪽 탐색창의 **관리** 섹션에서 **도메인 관리**를 클릭해 관련된 섹션을 확장한 다음 **내 도메인**을 클릭해 **내 도메인** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="b918c-172">![내 도메인](./media/active-directory-saas-jobscience-tutorial/ic767825.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="b918c-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="b918c-173">도메인이 올바르게 설정되었는지 확인하려면 “**Step 4 Deployed to Users**(4단계 사용자에게 배포)”에 있는지 확인하고 “**My Domain Settings**(내 도메인 설정)”을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="b918c-174">![사용자에게 배포된 도메인](./media/active-directory-saas-jobscience-tutorial/ic784377.png "사용자에게 배포된 도메인")</span><span class="sxs-lookup"><span data-stu-id="b918c-174">![Domain Deployed to User](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="b918c-175">Jobscience 회사 사이트에서 **보안 제어**를 클릭한 다음 **Single Sign-On 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="b918c-176">![보안 제어](./media/active-directory-saas-jobscience-tutorial/ic784364.png "보안 제어")</span><span class="sxs-lookup"><span data-stu-id="b918c-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="b918c-177">**Single Sign-On 설정** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-177">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="b918c-178">![Single Sign-On 설정](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="b918c-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="b918c-179">a.</span><span class="sxs-lookup"><span data-stu-id="b918c-179">a.</span></span> <span data-ttu-id="b918c-180">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="b918c-181">b.</span><span class="sxs-lookup"><span data-stu-id="b918c-181">b.</span></span> <span data-ttu-id="b918c-182">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-182">Click **New**.</span></span>

13. <span data-ttu-id="b918c-183">**SAML Single Sign-On 설정 편집** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="b918c-184">![SAML Single Sign-On 설정](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="b918c-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="b918c-185">a.</span><span class="sxs-lookup"><span data-stu-id="b918c-185">a.</span></span> <span data-ttu-id="b918c-186">**이름** 텍스트 상자에 구성할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-186">In the **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="b918c-187">b.</span><span class="sxs-lookup"><span data-stu-id="b918c-187">b.</span></span> <span data-ttu-id="b918c-188">**발급자** 텍스트 상자에 Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b918c-189">c.</span><span class="sxs-lookup"><span data-stu-id="b918c-189">c.</span></span> <span data-ttu-id="b918c-190">**엔터티 ID** 텍스트 상자에 `https://salesforce-jobscience.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="b918c-191">d.</span><span class="sxs-lookup"><span data-stu-id="b918c-191">d.</span></span> <span data-ttu-id="b918c-192">**찾아보기** 를 클릭하여 Azure AD 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-192">Click **Browse** to upload your Azure AD certificate.</span></span>

    <span data-ttu-id="b918c-193">e.</span><span class="sxs-lookup"><span data-stu-id="b918c-193">e.</span></span> <span data-ttu-id="b918c-194">**SAML ID 유형**으로 **사용자 개체에서 페더레이션 ID를 포함하는 어설션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>

    <span data-ttu-id="b918c-195">f.</span><span class="sxs-lookup"><span data-stu-id="b918c-195">f.</span></span> <span data-ttu-id="b918c-196">**SAML ID 위치**에서 **Subject 문의 NameIdentifier 요소에 ID 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>

    <span data-ttu-id="b918c-197">g.</span><span class="sxs-lookup"><span data-stu-id="b918c-197">g.</span></span> <span data-ttu-id="b918c-198">**ID 공급자 로그인 URL** 텍스트 상자에 Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b918c-199">h.</span><span class="sxs-lookup"><span data-stu-id="b918c-199">h.</span></span> <span data-ttu-id="b918c-200">**ID 공급자 로그인 URL** 텍스트 상자에 Azure Portal에서 복사한 **로그아웃 URL** 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b918c-201">i.</span><span class="sxs-lookup"><span data-stu-id="b918c-201">i.</span></span> <span data-ttu-id="b918c-202">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-202">Click **Save**.</span></span>

14. <span data-ttu-id="b918c-203">왼쪽 탐색창의 **관리** 섹션에서 **도메인 관리**를 클릭해 관련된 섹션을 확장한 다음 **내 도메인**을 클릭해 **내 도메인** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="b918c-204">![내 도메인](./media/active-directory-saas-jobscience-tutorial/ic767825.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="b918c-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="b918c-205">**내 도메인** 페이지의 **로그인 페이지 브랜딩** 섹션에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="b918c-206">![로그인 페이지 브랜딩](./media/active-directory-saas-jobscience-tutorial/ic767826.png "로그인 페이지 브랜딩")</span><span class="sxs-lookup"><span data-stu-id="b918c-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="b918c-207">**로그인 페이지 브랜딩** 페이지의 **인증 서비스** 섹션에 **SAML SSO 설정** 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="b918c-208">이름을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="b918c-209">![로그인 페이지 브랜딩](./media/active-directory-saas-jobscience-tutorial/ic784366.png "로그인 페이지 브랜딩")</span><span class="sxs-lookup"><span data-stu-id="b918c-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="b918c-210">서비스 공급자가 제공한 Single Sign-On URL을 가져오려면 **보안 제어** 메뉴 섹션의 **Single Sign On 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

    <span data-ttu-id="b918c-211">![보안 제어](./media/active-directory-saas-jobscience-tutorial/ic784368.png "보안 제어")</span><span class="sxs-lookup"><span data-stu-id="b918c-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="b918c-212">위 단계에서 만든 SSO 프로필을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-212">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="b918c-213">이 페이지에는 회사의 Single Sign-On URL(예: [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid))이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="b918c-214">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b918c-215">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b918c-216">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b918c-217">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b918c-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="b918c-218">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b918c-220">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="b918c-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b918c-221">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b918c-223">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b918c-225">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b918c-227">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b918c-229">a.</span><span class="sxs-lookup"><span data-stu-id="b918c-229">a.</span></span> <span data-ttu-id="b918c-230">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b918c-231">b.</span><span class="sxs-lookup"><span data-stu-id="b918c-231">b.</span></span> <span data-ttu-id="b918c-232">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b918c-233">c.</span><span class="sxs-lookup"><span data-stu-id="b918c-233">c.</span></span> <span data-ttu-id="b918c-234">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b918c-235">d.</span><span class="sxs-lookup"><span data-stu-id="b918c-235">d.</span></span> <span data-ttu-id="b918c-236">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="b918c-237">Jobscience 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b918c-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="b918c-238">Azure AD 사용자가 Jobscience에 로그인할 수 있도록 하려면 Jobscience로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="b918c-239">Jobscience의 경우 프로비저닝은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-239">In the case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="b918c-240">다른 Jobscience 사용자 계정 생성 도구 또는 Jobscience가 제공한 API를 사용하여 Azure Active Directory 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="b918c-241">**사용자 프로비전을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b918c-241">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="b918c-242">**Jobscience** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-242">Log in to your **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="b918c-243">설정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-243">Go to Setup.</span></span>
   
   <span data-ttu-id="b918c-244">![설치](./media/active-directory-saas-jobscience-tutorial/ic784358.png "설치")</span><span class="sxs-lookup"><span data-stu-id="b918c-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="b918c-245">**사용자 관리 \> 사용자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-245">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="b918c-246">![사용자](./media/active-directory-saas-jobscience-tutorial/ic784369.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="b918c-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="b918c-247">**새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-247">Click **New User**.</span></span>
   
   <span data-ttu-id="b918c-248">![모든 사용자](./media/active-directory-saas-jobscience-tutorial/ic784370.png "모든 사용자")</span><span class="sxs-lookup"><span data-stu-id="b918c-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="b918c-249">**사용자 편집** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-249">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="b918c-250">![사용자 편집](./media/active-directory-saas-jobscience-tutorial/ic784371.png "사용자 편집")</span><span class="sxs-lookup"><span data-stu-id="b918c-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="b918c-251">a.</span><span class="sxs-lookup"><span data-stu-id="b918c-251">a.</span></span> <span data-ttu-id="b918c-252">**First Name**(이름) 텍스트 상자에 사용자의 이름(예: Britta)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-252">In the **First Name** textbox, type a first name of the user like Britta.</span></span>
   
   <span data-ttu-id="b918c-253">b.</span><span class="sxs-lookup"><span data-stu-id="b918c-253">b.</span></span> <span data-ttu-id="b918c-254">**Last Name**(성) 텍스트 상자에 사용자의 성(예: Simon)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-254">In the **Last Name** textbox, type a last name of the user like Simon.</span></span>
   
   <span data-ttu-id="b918c-255">c.</span><span class="sxs-lookup"><span data-stu-id="b918c-255">c.</span></span> <span data-ttu-id="b918c-256">**Alias**(별칭) 텍스트 상자에 사용자의 별칭(예: brittas)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-256">In the **Alias** textbox, type an alias name of the user like brittas.</span></span>

   <span data-ttu-id="b918c-257">d.</span><span class="sxs-lookup"><span data-stu-id="b918c-257">d.</span></span> <span data-ttu-id="b918c-258">**전자 메일** 텍스트 상자에서 Brittasimon@contoso.com과 같은 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="b918c-259">e.</span><span class="sxs-lookup"><span data-stu-id="b918c-259">e.</span></span> <span data-ttu-id="b918c-260">**User Name**(사용자 이름) 텍스트 상자에 사용자의 사용자 이름(예: Brittasimon@contoso.com)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="b918c-261">f.</span><span class="sxs-lookup"><span data-stu-id="b918c-261">f.</span></span> <span data-ttu-id="b918c-262">**Nick Name**(애칭) 텍스트 상자에 사용자의 애칭(예: Simon)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="b918c-263">g.</span><span class="sxs-lookup"><span data-stu-id="b918c-263">g.</span></span> <span data-ttu-id="b918c-264">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="b918c-265">Azure Active Directory 계정 소유자가 이메일을 받아서 여기에 포함된 링크를 클릭하여 계정을 확인하면 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b918c-266">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="b918c-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b918c-267">이 섹션에서는 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 Jobscience에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b918c-269">**Britta Simon을 Jobscience에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="b918c-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="b918c-270">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b918c-272">응용 프로그램 목록에서 **Jobscience**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-272">In the applications list, select **Jobscience**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="b918c-274">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-274">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b918c-276">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-276">Click **Add** button.</span></span> <span data-ttu-id="b918c-277">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b918c-279">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b918c-280">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b918c-281">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b918c-282">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b918c-282">Testing single sign-on</span></span>

<span data-ttu-id="b918c-283">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b918c-284">액세스 패널에서 Jobscience 타일을 클릭하면 Jobscience 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="b918c-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span></span>
<span data-ttu-id="b918c-285">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b918c-285">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b918c-286">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b918c-286">Additional resources</span></span>

* [<span data-ttu-id="b918c-287">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="b918c-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b918c-288">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b918c-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png


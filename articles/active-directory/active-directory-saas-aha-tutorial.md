---
title: "자습서: Aha!와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Aha! 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7723864b2e1ab2d5b69d86f0fa18416b9d3f9aa3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="79362-104">자습서: Aha!와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="79362-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="79362-105">이 자습서에서는 Aha를 통합 하는 방법에 설명!</span><span class="sxs-lookup"><span data-stu-id="79362-105">In this tutorial, you learn how to integrate Aha!</span></span> <span data-ttu-id="79362-106">azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79362-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79362-107">통합 Aha!</span><span class="sxs-lookup"><span data-stu-id="79362-107">Integrating Aha!</span></span> <span data-ttu-id="79362-108">Azure AD에는 다음과 같은 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-108">with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="79362-109">Aha!에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79362-109">You can control in Azure AD who has access to Aha!</span></span>
- <span data-ttu-id="79362-110">사용자가 자동으로 Aha!에 로그온하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79362-110">You can enable your users to automatically get signed-on to Aha!</span></span> <span data-ttu-id="79362-111">Azure AD 계정이 포함된 (Single Sign-On)</span><span class="sxs-lookup"><span data-stu-id="79362-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79362-112">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79362-112">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="79362-113">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79362-113">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79362-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="79362-114">Prerequisites</span></span>

<span data-ttu-id="79362-115">Aha!와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-115">To configure Azure AD integration with Aha!, you need the following items:</span></span>

- <span data-ttu-id="79362-116">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="79362-116">An Azure AD subscription</span></span>
- <span data-ttu-id="79362-117">Aha!</span><span class="sxs-lookup"><span data-stu-id="79362-117">An Aha!</span></span> <span data-ttu-id="79362-118">Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="79362-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79362-119">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="79362-119">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79362-120">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-120">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79362-121">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="79362-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79362-122">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79362-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79362-123">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="79362-123">Scenario description</span></span>
<span data-ttu-id="79362-124">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79362-125">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79362-125">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79362-126">추가 Aha!</span><span class="sxs-lookup"><span data-stu-id="79362-126">Adding Aha!</span></span> <span data-ttu-id="79362-127">갤러리에서</span><span class="sxs-lookup"><span data-stu-id="79362-127">from the gallery</span></span>
2. <span data-ttu-id="79362-128">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="79362-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-the-gallery"></a><span data-ttu-id="79362-129">추가 Aha!</span><span class="sxs-lookup"><span data-stu-id="79362-129">Adding Aha!</span></span> <span data-ttu-id="79362-130">갤러리에서</span><span class="sxs-lookup"><span data-stu-id="79362-130">from the gallery</span></span>
<span data-ttu-id="79362-131">통합을 구성 하는의 Aha!</span><span class="sxs-lookup"><span data-stu-id="79362-131">To configure the integration of Aha!</span></span> <span data-ttu-id="79362-132">Azure AD로 Aha 추가 해야!</span><span class="sxs-lookup"><span data-stu-id="79362-132">into Azure AD, you need to add Aha!</span></span> <span data-ttu-id="79362-133">관리 되는 SaaS 앱 목록에 갤러리입니다.</span><span class="sxs-lookup"><span data-stu-id="79362-133">from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79362-134">**갤러리에서 Aha!를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="79362-134">**To add Aha! from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79362-135">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-135">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79362-137">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-137">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="79362-138">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-138">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="79362-140">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-140">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="79362-142">검색 상자에 **Aha!**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-142">In the search box, type **Aha!**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="79362-144">결과 패널에서 **Aha!**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-144">In the results panel, select **Aha!**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79362-146">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="79362-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79362-147">이 섹션에서는 구성 및 Azure AD single sign-on 테스트와 Aha!</span><span class="sxs-lookup"><span data-stu-id="79362-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="79362-148">"Britta Simon." 이라는 테스트 사용자</span><span class="sxs-lookup"><span data-stu-id="79362-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="79362-149">Single sign-on 작업에 대 한 Azure AD 알아야 어떤 테이블에 해당 사용자에 Aha!</span><span class="sxs-lookup"><span data-stu-id="79362-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Aha!</span></span> <span data-ttu-id="79362-150">Azure AD에서 사용자에 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79362-150">is to a user in Azure AD.</span></span> <span data-ttu-id="79362-151">즉, Azure AD 사용자 및 관련된 사용자 Aha에 간의 링크 관계가!</span><span class="sxs-lookup"><span data-stu-id="79362-151">In other words, a link relationship between an Azure AD user and the related user in Aha!</span></span> <span data-ttu-id="79362-152">설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-152">needs to be established.</span></span>

<span data-ttu-id="79362-153">Aha!에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-153">In Aha!, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="79362-154">Aha!에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-154">To configure and test Azure AD single sign-on with Aha!, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79362-155">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="79362-156">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79362-157">**[만들기는 Aha! 테스트 사용자](#creating-an-aha-test-user)**  -Aha의 Britta Simon 상응 하는 것으로!</span><span class="sxs-lookup"><span data-stu-id="79362-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - to have a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="79362-158">사용자의 Azure AD 표현에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79362-158">that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="79362-159">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79362-160">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79362-161">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="79362-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79362-162">이 섹션에서는 Azure AD에서 single sign-on Azure 포털에서 설정 및 Aha에서 single sign on 구성!</span><span class="sxs-lookup"><span data-stu-id="79362-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="79362-163">응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="79362-163">application.</span></span>

<span data-ttu-id="79362-164">**Aha!에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="79362-164">**To configure Azure AD single sign-on with Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="79362-165">Azure 포털에서에 **Aha!**</span><span class="sxs-lookup"><span data-stu-id="79362-165">In the Azure portal, on the **Aha!**</span></span> <span data-ttu-id="79362-166">응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-166">application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="79362-168">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-168">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="79362-170">에 **Aha! 도메인 및 Url** 섹션에서 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-170">On the **Aha! Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="79362-172">a.</span><span class="sxs-lookup"><span data-stu-id="79362-172">a.</span></span> <span data-ttu-id="79362-173">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="79362-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="79362-174">b.</span><span class="sxs-lookup"><span data-stu-id="79362-174">b.</span></span> <span data-ttu-id="79362-175">**식별자** 텍스트 상자에서 `https://<companyname>.aha.io` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-175">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79362-176">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="79362-176">These values are not real.</span></span> <span data-ttu-id="79362-177">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-177">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="79362-178">연락처 [Aha! 클라이언트 지원 팀](https://www.aha.io/company/contact) 이러한 값을 가져오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="79362-179">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="79362-181">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-181">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79362-183">다른 웹 브라우저 창에서 Aha!</span><span class="sxs-lookup"><span data-stu-id="79362-183">In a different web browser window, log in to your Aha!</span></span> <span data-ttu-id="79362-184">회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-184">company site as an administrator.</span></span>

7. <span data-ttu-id="79362-185">위쪽의 메뉴에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-185">In the menu on the top, click **Settings**.</span></span>

    <span data-ttu-id="79362-186">![설정](./media/active-directory-saas-aha-tutorial/IC798950.png "설정")</span><span class="sxs-lookup"><span data-stu-id="79362-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="79362-187">**계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-187">Click **Account**.</span></span>
   
    <span data-ttu-id="79362-188">![프로필](./media/active-directory-saas-aha-tutorial/IC798951.png "프로필")</span><span class="sxs-lookup"><span data-stu-id="79362-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="79362-189">**보안 및 single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="79362-190">![보안 및 Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798952.png "보안 및 Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="79362-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="79362-191">**Single Sign-On** 섹션에서 **ID 공급자**로 **SAML2.0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="79362-192">![보안 및 Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798953.png "보안 및 Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="79362-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="79362-193">**Single Sign-On** 구성 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-193">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
    
    <span data-ttu-id="79362-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="79362-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="79362-195">a.</span><span class="sxs-lookup"><span data-stu-id="79362-195">a.</span></span> <span data-ttu-id="79362-196">**이름** 텍스트 상자에 구성할 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-196">In the **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="79362-197">b.</span><span class="sxs-lookup"><span data-stu-id="79362-197">b.</span></span> <span data-ttu-id="79362-198">**구성 사용 형식**에 **메타데이터 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="79362-199">c.</span><span class="sxs-lookup"><span data-stu-id="79362-199">c.</span></span> <span data-ttu-id="79362-200">다운로드한 메타데이터 파일을 업로드하려면 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-200">To upload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="79362-201">d.</span><span class="sxs-lookup"><span data-stu-id="79362-201">d.</span></span> <span data-ttu-id="79362-202">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="79362-203">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79362-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="79362-204">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79362-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="79362-205">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79362-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79362-206">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="79362-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="79362-207">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="79362-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="79362-209">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="79362-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79362-210">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79362-212">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79362-214">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79362-216">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79362-218">a.</span><span class="sxs-lookup"><span data-stu-id="79362-218">a.</span></span> <span data-ttu-id="79362-219">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79362-220">b.</span><span class="sxs-lookup"><span data-stu-id="79362-220">b.</span></span> <span data-ttu-id="79362-221">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79362-222">c.</span><span class="sxs-lookup"><span data-stu-id="79362-222">c.</span></span> <span data-ttu-id="79362-223">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="79362-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="79362-224">d.</span><span class="sxs-lookup"><span data-stu-id="79362-224">d.</span></span> <span data-ttu-id="79362-225">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="79362-226">만들기는 Aha!</span><span class="sxs-lookup"><span data-stu-id="79362-226">Creating an Aha!</span></span> <span data-ttu-id="79362-227">테스트 사용자</span><span class="sxs-lookup"><span data-stu-id="79362-227">test user</span></span>

<span data-ttu-id="79362-228">Azure AD 사용자가 Aha!에 로그인할 수 있도록 하려면 Aha!로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-228">To enable Azure AD users to log in to Aha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="79362-229">Aha!의 경우 프로비전은 자동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="79362-229">In the case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="79362-230">작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79362-230">There is no action item for you.</span></span>

<span data-ttu-id="79362-231">필요한 경우 첫 번째 Single Sign-On 시도에서 사용자가 자동으로 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79362-231">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="79362-232">다른 Aha! 사용자 계정 생성 도구</span><span class="sxs-lookup"><span data-stu-id="79362-232">You can use any other Aha!</span></span> <span data-ttu-id="79362-233">또는 Aha!가 제공한 API를 사용하여 AAD 사용자 계정을</span><span class="sxs-lookup"><span data-stu-id="79362-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="79362-234">프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79362-234">to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="79362-235">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="79362-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="79362-236">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Aha!에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-236">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aha!.</span></span>

![사용자 할당][200] 

<span data-ttu-id="79362-238">**Britta Simon을 Aha!에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="79362-238">**To assign Britta Simon to Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="79362-239">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-239">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="79362-241">응용 프로그램 목록에서 **Aha!**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-241">In the applications list, select **Aha!**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="79362-243">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-243">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="79362-245">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-245">Click **Add** button.</span></span> <span data-ttu-id="79362-246">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="79362-248">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="79362-249">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79362-250">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79362-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79362-251">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="79362-251">Testing single sign-on</span></span>

<span data-ttu-id="79362-252">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="79362-252">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="79362-253">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79362-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79362-254">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="79362-254">Additional resources</span></span>

* [<span data-ttu-id="79362-255">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="79362-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79362-256">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="79362-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png


---
title: "자습서: Adaptive Suite와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 적응 제품군 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="ebf84-103">자습서: Adaptive Suite와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="ebf84-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="ebf84-104">이 자습서에 설명 어떻게 toointegrate 적응 Suite Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ebf84-104">In this tutorial, you learn how toointegrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ebf84-105">적응 Suite Azure AD와 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-105">Integrating Adaptive Suite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ebf84-106">액세스 tooAdaptive 도구 모음을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-106">You can control in Azure AD who has access tooAdaptive Suite</span></span>
- <span data-ttu-id="ebf84-107">프로그램 사용자 tooautomatically get 로그온 tooAdaptive (Single Sign-on) 제품군으로는 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-107">You can enable your users tooautomatically get signed-on tooAdaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ebf84-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ebf84-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebf84-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ebf84-110">Prerequisites</span></span>

<span data-ttu-id="ebf84-111">적응 도구 모음과 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-111">tooconfigure Azure AD integration with Adaptive Suite, you need hello following items:</span></span>

- <span data-ttu-id="ebf84-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="ebf84-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ebf84-113">Adaptive Suite Single-Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="ebf84-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ebf84-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ebf84-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ebf84-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ebf84-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ebf84-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ebf84-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="ebf84-118">Scenario description</span></span>
<span data-ttu-id="ebf84-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ebf84-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ebf84-121">적응 Suite hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="ebf84-121">Adding Adaptive Suite from hello gallery</span></span>
2. <span data-ttu-id="ebf84-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ebf84-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-hello-gallery"></a><span data-ttu-id="ebf84-123">적응 Suite hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="ebf84-123">Adding Adaptive Suite from hello gallery</span></span>
<span data-ttu-id="ebf84-124">tooconfigure hello와의 통합 적응 Suite Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 적응 Suite tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-124">tooconfigure hello integration of Adaptive Suite into Azure AD, you need tooadd Adaptive Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ebf84-125">**hello 갤러리의 적응 Suite tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ebf84-125">**tooadd Adaptive Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebf84-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ebf84-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ebf84-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="ebf84-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="ebf84-133">Hello 검색 상자에 입력 **적응 Suite**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-133">In hello search box, type **Adaptive Suite**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="ebf84-135">Hello 결과 패널에서 선택 **적응 Suite**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-135">In hello results panel, select **Adaptive Suite**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ebf84-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ebf84-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ebf84-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Adaptive Suite에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ebf84-139">Single sign on toowork에 대 한 Azure AD는 tooknow 적응 도구 모음에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adaptive Suite is tooa user in Azure AD.</span></span> <span data-ttu-id="ebf84-140">즉, Azure AD 사용자 및 hello 적응 도구 모음에서 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-140">In other words, a link relationship between an Azure AD user and hello related user in Adaptive Suite needs toobe established.</span></span>

<span data-ttu-id="ebf84-141">적응 도구 모음에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-141">In Adaptive Suite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ebf84-142">tooconfigure 및 적응 Suite를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-142">tooconfigure and test Azure AD single sign-on with Adaptive Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ebf84-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ebf84-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ebf84-145">**[적응 Suite 테스트 사용자 만들기](#creating-an-adaptive-suite-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 적응 도구 모음에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - toohave a counterpart of Britta Simon in Adaptive Suite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ebf84-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ebf84-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="ebf84-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ebf84-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="ebf84-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ebf84-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 적응 Suite 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="ebf84-150">**tooconfigure Azure AD single sign on 적응 도구 모음을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ebf84-150">**tooconfigure Azure AD single sign-on with Adaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebf84-151">Hello hello에 Azure 포털에서에서 **적응 Suite** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-151">In hello Azure portal, on hello **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="ebf84-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="ebf84-155">Hello에 **적응 Suite 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-155">On hello **Adaptive Suite Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="ebf84-157">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="ebf84-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="ebf84-158">Hello 적응 제품군의에서이 값을 가져올 수 있습니다 **SAML SSO 설정** 페이지.</span><span class="sxs-lookup"><span data-stu-id="ebf84-158">You can get this value from hello Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="ebf84-159">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="ebf84-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-161">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ebf84-163">Hello에 **적응 Suite 구성** 섹션에서 클릭 **적응 Suite 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="ebf84-163">On hello **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ebf84-164">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="ebf84-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="ebf84-166">다른 웹 브라우저 창에서 관리자 권한으로 tooyour 적응 Suite 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-166">In a different web browser window, log in tooyour Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="ebf84-167">너무 이동**Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-167">Go too**Admin**.</span></span>
   
    <span data-ttu-id="ebf84-168">![관리자](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="ebf84-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="ebf84-169">Hello에 **사용자 및 역할** 섹션에서 클릭 **SAML SSO 설정 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-169">In hello **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="ebf84-170">![SAML SSO 설정 관리](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "SAML SSO 설정 관리")</span><span class="sxs-lookup"><span data-stu-id="ebf84-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="ebf84-171">Hello에 **SAML SSO 설정** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-171">On hello **SAML SSO Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="ebf84-172">![SAML SSO 설정](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO 설정")</span><span class="sxs-lookup"><span data-stu-id="ebf84-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="ebf84-173">a.</span><span class="sxs-lookup"><span data-stu-id="ebf84-173">a.</span></span> <span data-ttu-id="ebf84-174">Hello에 **Id 공급자 이름** 텍스트 상자, 구성에 대 한 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-174">In hello **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="ebf84-175">b.</span><span class="sxs-lookup"><span data-stu-id="ebf84-175">b.</span></span> <span data-ttu-id="ebf84-176">붙여넣기 hello **SAML 엔터티 ID** 값이 hello에 Azure 포털에서 복사 **Id 공급자 엔터티 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-176">Paste hello **SAML Entity ID** value copied from Azure portal into hello **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="ebf84-177">c.</span><span class="sxs-lookup"><span data-stu-id="ebf84-177">c.</span></span> <span data-ttu-id="ebf84-178">붙여넣기 hello **SAML Single Sign-on 서비스 URL** 값이 hello에 Azure 포털에서 복사 **Id 공급자 SSO URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-178">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="ebf84-179">d.</span><span class="sxs-lookup"><span data-stu-id="ebf84-179">d.</span></span> <span data-ttu-id="ebf84-180">붙여넣기 hello **SAML Single Sign-on 서비스 URL** 값이 hello에 Azure 포털에서 복사 **사용자 지정 로그 아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-180">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="ebf84-181">e.</span><span class="sxs-lookup"><span data-stu-id="ebf84-181">e.</span></span> <span data-ttu-id="ebf84-182">tooupload 다운로드 한 인증서를 클릭 하 여 **파일 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-182">tooupload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="ebf84-183">f.</span><span class="sxs-lookup"><span data-stu-id="ebf84-183">f.</span></span> <span data-ttu-id="ebf84-184">에 대 한 hello 다음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-184">Select hello following, for:</span></span>
    * <span data-ttu-id="ebf84-185">**SAML 사용자 ID**에 대해 **사용자의 Adaptive Insights 사용자 이름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="ebf84-186">**SAML 사용자 ID 위치**에 대해 **제목의 NameID에서 사용자 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="ebf84-187">**SAML NameID 형식**에 대해 **전자 메일 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="ebf84-188">**SAML 사용**에 대해 **SAML SSO 및 Adaptive Insights 직접 로그인 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="ebf84-189">g.</span><span class="sxs-lookup"><span data-stu-id="ebf84-189">g.</span></span> <span data-ttu-id="ebf84-190">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ebf84-191">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="ebf84-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ebf84-192">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="ebf84-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ebf84-193">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ebf84-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ebf84-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ebf84-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="ebf84-195">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="ebf84-197">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ebf84-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebf84-198">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ebf84-200">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ebf84-202">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ebf84-204">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ebf84-206">a.</span><span class="sxs-lookup"><span data-stu-id="ebf84-206">a.</span></span> <span data-ttu-id="ebf84-207">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ebf84-208">b.</span><span class="sxs-lookup"><span data-stu-id="ebf84-208">b.</span></span> <span data-ttu-id="ebf84-209">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ebf84-210">c.</span><span class="sxs-lookup"><span data-stu-id="ebf84-210">c.</span></span> <span data-ttu-id="ebf84-211">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ebf84-212">d.</span><span class="sxs-lookup"><span data-stu-id="ebf84-212">d.</span></span> <span data-ttu-id="ebf84-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="ebf84-214">Adaptive Suite 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ebf84-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="ebf84-215">tooenable Azure AD 사용자가 toolog tooAdaptive Suite에서에서은 프로 비전 해야 적응 도구 모음으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-215">tooenable Azure AD users toolog in tooAdaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="ebf84-216">Hello 적응 Suite의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-216">In hello case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="ebf84-217">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="ebf84-217">**tooconfigure user provisioning, perform hello following steps:**</span></span> 

1. <span data-ttu-id="ebf84-218">Tooyour 로그인 **적응 Suite** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-218">Log in tooyour **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="ebf84-219">너무 이동**Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-219">Go too**Admin**.</span></span>
   
   <span data-ttu-id="ebf84-220">![관리자](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="ebf84-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="ebf84-221">Hello에 **사용자 및 역할** 섹션에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-221">In hello **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="ebf84-222">![사용자 추가](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="ebf84-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="ebf84-223">Hello에 **새 사용자** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-223">In hello **New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="ebf84-224">![제출](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "제출")</span><span class="sxs-lookup"><span data-stu-id="ebf84-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="ebf84-225">a.</span><span class="sxs-lookup"><span data-stu-id="ebf84-225">a.</span></span> <span data-ttu-id="ebf84-226">형식 hello **이름**, **로그인**, **전자 메일**, **암호** 유효한 Azure Active Directory 사용자의 관련 hello에 tooprovision 복원할 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-226">Type hello **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
  
   <span data-ttu-id="ebf84-227">b.</span><span class="sxs-lookup"><span data-stu-id="ebf84-227">b.</span></span> <span data-ttu-id="ebf84-228">**역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="ebf84-229">c.</span><span class="sxs-lookup"><span data-stu-id="ebf84-229">c.</span></span> <span data-ttu-id="ebf84-230">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="ebf84-231">다른 적응 Suite 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 적응 Suite tooprovision에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ebf84-232">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ebf84-233">이 섹션에서는 액세스 tooAdaptive 제품군을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdaptive Suite.</span></span>

![사용자 할당][200] 

<span data-ttu-id="ebf84-235">**tooassign Britta Simon tooAdaptive 도구 모음을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ebf84-235">**tooassign Britta Simon tooAdaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="ebf84-236">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="ebf84-238">Hello 응용 프로그램 목록에서 선택 **적응 Suite**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-238">In hello applications list, select **Adaptive Suite**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="ebf84-240">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="ebf84-242">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-242">Click **Add** button.</span></span> <span data-ttu-id="ebf84-243">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="ebf84-245">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ebf84-246">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ebf84-247">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ebf84-248">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="ebf84-248">Testing single sign-on</span></span>

<span data-ttu-id="ebf84-249">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 하 여 Microsoft Azure AD Single Sign-on 사용 하 여 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-249">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="ebf84-250">Hello 액세스 패널에서에서 hello 적응 Suite 타일을 클릭할 때 자동으로 로그온 tooyour 적응 Suite 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf84-250">When you click hello Adaptive Suite tile in hello Access Panel, you should get automatically signed-on tooyour Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ebf84-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ebf84-251">Additional resources</span></span>

* [<span data-ttu-id="ebf84-252">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="ebf84-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ebf84-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ebf84-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png


---
title: "자습서: Rightscale과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Rightscale 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="53a36-103">자습서: Rightscale과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="53a36-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="53a36-104">이 자습서에 설명 어떻게 toointegrate Rightscale Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="53a36-104">In this tutorial, you learn how toointegrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53a36-105">다음 이점을 hello로 제공 Rightscale Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="53a36-105">Integrating Rightscale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="53a36-106">액세스 tooRightscale을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-106">You can control in Azure AD who has access tooRightscale</span></span>
- <span data-ttu-id="53a36-107">프로그램 사용자 tooautomatically get 로그온 tooRightscale (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-107">You can enable your users tooautomatically get signed-on tooRightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="53a36-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="53a36-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53a36-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="53a36-110">Prerequisites</span></span>

<span data-ttu-id="53a36-111">다음 항목 hello가 필요 tooconfigure Rightscale와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-111">tooconfigure Azure AD integration with Rightscale, you need hello following items:</span></span>

- <span data-ttu-id="53a36-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="53a36-112">An Azure AD subscription</span></span>
- <span data-ttu-id="53a36-113">Rightscale Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="53a36-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="53a36-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="53a36-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="53a36-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="53a36-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="53a36-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="53a36-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="53a36-118">Scenario description</span></span>
<span data-ttu-id="53a36-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53a36-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="53a36-121">Rightscale는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="53a36-121">Adding Rightscale from hello gallery</span></span>
2. <span data-ttu-id="53a36-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="53a36-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-hello-gallery"></a><span data-ttu-id="53a36-123">Rightscale는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="53a36-123">Adding Rightscale from hello gallery</span></span>
<span data-ttu-id="53a36-124">tooconfigure hello와의 통합 Rightscale Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Rightscale tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-124">tooconfigure hello integration of Rightscale into Azure AD, you need tooadd Rightscale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="53a36-125">**hello 갤러리에서 Rightscale tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="53a36-125">**tooadd Rightscale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="53a36-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="53a36-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="53a36-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="53a36-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="53a36-133">Hello 검색 상자에 입력 **Rightscale**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-133">In hello search box, type **Rightscale**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="53a36-135">Hello 결과 패널에서 선택 **Rightscale**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-135">In hello results panel, select **Rightscale**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="53a36-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="53a36-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="53a36-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Rightscale에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="53a36-139">Single sign on toowork에 대 한 Azure AD는 tooknow Rightscale에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rightscale is tooa user in Azure AD.</span></span> <span data-ttu-id="53a36-140">즉, Azure AD 사용자 및 Rightscale에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-140">In other words, a link relationship between an Azure AD user and hello related user in Rightscale needs toobe established.</span></span>

<span data-ttu-id="53a36-141">Rightscale에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-141">In Rightscale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="53a36-142">tooconfigure 및 Rightscale 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-142">tooconfigure and test Azure AD single sign-on with Rightscale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="53a36-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="53a36-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53a36-145">**[Rightscale 테스트 사용자 만들기](#creating-a-rightscale-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Rightscale에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - toohave a counterpart of Britta Simon in Rightscale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="53a36-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53a36-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="53a36-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="53a36-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="53a36-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="53a36-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Rightscale 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="53a36-150">**tooconfigure Azure AD single sign on, Rightscale와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="53a36-150">**tooconfigure Azure AD single sign-on with Rightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="53a36-151">Hello hello에 Azure 포털에서에서 **Rightscale** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-151">In hello Azure portal, on hello **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="53a36-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="53a36-155">Hello에 **Rightscale 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP 시작 모드** 없는 tooperform 단계 hello 앱은 Azure와 사전 통합 이미으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-155">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode** you do not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="53a36-157">Hello에 **Rightscale 도메인 및 Url** 섹션 tooconfigure hello 응용 프로그램에 필요한 경우 **SP 시작 모드**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-157">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="53a36-159">a.</span><span class="sxs-lookup"><span data-stu-id="53a36-159">a.</span></span> <span data-ttu-id="53a36-160">Hello 클릭 **고급 URL 설정 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-160">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="53a36-161">b.</span><span class="sxs-lookup"><span data-stu-id="53a36-161">b.</span></span> <span data-ttu-id="53a36-162">Hello에 **로그온 URL** textbox hello URL 입력:`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="53a36-162">In hello **Sign On URL** textbox, type hello URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="53a36-163">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-163">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="53a36-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-165">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="53a36-167">Hello에 **Rightscale 구성** 섹션에서 클릭 **구성 Rightscale** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="53a36-167">On hello **Rightscale Configuration** section, click **Configure Rightscale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="53a36-168">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="53a36-168">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="53a36-169">![Single Sign-On 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="53a36-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="53a36-170">SSO 응용 프로그램에 대해 구성 된 tooget toosign에 tooyour RightScale 테 넌 트 관리자 권한으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-170">tooget SSO configured for your application, you need toosign-on tooyour RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="53a36-171">a.</span><span class="sxs-lookup"><span data-stu-id="53a36-171">a.</span></span> <span data-ttu-id="53a36-172">Hello 메뉴에서 hello 위에 표시를 클릭 hello **설정** 탭을 선택한 **Single Sign On**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="53a36-174">b.</span><span class="sxs-lookup"><span data-stu-id="53a36-174">b.</span></span> <span data-ttu-id="53a36-175">Hello 클릭 "**새**" 단추 tooadd **Your SAML Id 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-175">Click hello "**new**" button tooadd **Your SAML Identity Providers**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="53a36-177">c.</span><span class="sxs-lookup"><span data-stu-id="53a36-177">c.</span></span> <span data-ttu-id="53a36-178">hello 텍스트 상자에 **표시 이름**, 회사 이름을 입력 하십시오.</span><span class="sxs-lookup"><span data-stu-id="53a36-178">In hello textbox of **Display Name**, input your company name.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="53a36-180">d.</span><span class="sxs-lookup"><span data-stu-id="53a36-180">d.</span></span> <span data-ttu-id="53a36-181">선택 **검색 힌트를 사용 하 여 허용 RightScale에서 시작한 SSO** 입력 하 고 프로그램 **도메인 이름** hello 텍스트 상자 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in hello below textbox.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="53a36-183">e.</span><span class="sxs-lookup"><span data-stu-id="53a36-183">e.</span></span> <span data-ttu-id="53a36-184">Hello 값을 붙여 **SAML Single Sign-on 서비스 URL** 에 Azure 포털에서 복사한 있는 **SAML SSO 끝점** RightScale에 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-184">Paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="53a36-186">f.</span><span class="sxs-lookup"><span data-stu-id="53a36-186">f.</span></span> <span data-ttu-id="53a36-187">Hello 값을 붙여 **SAML 엔터티 ID** 에 Azure 포털에서 복사한 있는 **SAML EntityID** RightScale에 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-187">Paste hello value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="53a36-189">g.</span><span class="sxs-lookup"><span data-stu-id="53a36-189">g.</span></span> <span data-ttu-id="53a36-190">클릭 **브라우저** 단추 tooupload hello 인증서를 Azure 포털에서 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-190">Click **Browser** button tooupload hello certificate which you downloaded from Azure portal.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="53a36-192">h.</span><span class="sxs-lookup"><span data-stu-id="53a36-192">h.</span></span> <span data-ttu-id="53a36-193">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="53a36-194">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="53a36-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="53a36-195">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="53a36-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="53a36-196">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="53a36-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="53a36-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="53a36-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="53a36-198">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="53a36-200">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="53a36-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="53a36-201">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="53a36-203">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="53a36-205">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="53a36-207">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="53a36-209">a.</span><span class="sxs-lookup"><span data-stu-id="53a36-209">a.</span></span> <span data-ttu-id="53a36-210">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53a36-211">b.</span><span class="sxs-lookup"><span data-stu-id="53a36-211">b.</span></span> <span data-ttu-id="53a36-212">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="53a36-213">c.</span><span class="sxs-lookup"><span data-stu-id="53a36-213">c.</span></span> <span data-ttu-id="53a36-214">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="53a36-215">d.</span><span class="sxs-lookup"><span data-stu-id="53a36-215">d.</span></span> <span data-ttu-id="53a36-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="53a36-217">Rightscale 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="53a36-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="53a36-218">이 섹션에서는 RightScale에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="53a36-219">작업할 [Rightscale 클라이언트 지원 팀](mailto:support@rightscale.com) hello RightScale 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) tooadd hello users in hello RightScale platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="53a36-220">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="53a36-221">이 섹션에서는 tooRightscale 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightscale.</span></span>

![사용자 할당][200] 

<span data-ttu-id="53a36-223">**tooassign Britta Simon tooRightscale hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="53a36-223">**tooassign Britta Simon tooRightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="53a36-224">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="53a36-226">Hello 응용 프로그램 목록에서 선택 **Rightscale**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-226">In hello applications list, select **Rightscale**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="53a36-228">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="53a36-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-230">Click **Add** button.</span></span> <span data-ttu-id="53a36-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="53a36-233">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="53a36-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="53a36-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="53a36-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="53a36-236">Testing single sign-on</span></span>

<span data-ttu-id="53a36-237">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="53a36-238">Hello 액세스 패널에서에서 hello RightScale 타일을 클릭할 때 자동으로 로그온 tooyour RightScale 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a36-238">When you click hello RightScale tile in hello Access Panel, you should get automatically signed-on tooyour RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53a36-239">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="53a36-239">Additional resources</span></span>

* [<span data-ttu-id="53a36-240">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="53a36-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53a36-241">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="53a36-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png


---
title: "자습서: LCVista와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 LCVista 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="b737d-103">자습서: LCVista와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b737d-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="b737d-104">이 자습서에 설명 어떻게 toointegrate LCVista Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b737d-104">In this tutorial, you learn how toointegrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b737d-105">다음 이점을 hello로 제공 LCVista Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="b737d-105">Integrating LCVista with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b737d-106">액세스 tooLCVista을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-106">You can control in Azure AD who has access tooLCVista</span></span>
- <span data-ttu-id="b737d-107">프로그램 사용자 tooautomatically get 로그온 tooLCVista (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-107">You can enable your users tooautomatically get signed-on tooLCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b737d-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b737d-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b737d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b737d-110">Prerequisites</span></span>

<span data-ttu-id="b737d-111">다음 항목 hello가 필요 tooconfigure LCVista와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-111">tooconfigure Azure AD integration with LCVista, you need hello following items:</span></span>

- <span data-ttu-id="b737d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b737d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b737d-113">LCVista Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b737d-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b737d-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b737d-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b737d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b737d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b737d-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b737d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b737d-118">Scenario description</span></span>
<span data-ttu-id="b737d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b737d-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b737d-121">LCVista는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b737d-121">Adding LCVista from hello gallery</span></span>
2. <span data-ttu-id="b737d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b737d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-hello-gallery"></a><span data-ttu-id="b737d-123">LCVista는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b737d-123">Adding LCVista from hello gallery</span></span>
<span data-ttu-id="b737d-124">tooconfigure hello와의 통합 LCVista Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 LCVista tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-124">tooconfigure hello integration of LCVista into Azure AD, you need tooadd LCVista from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b737d-125">**hello 갤러리에서 LCVista tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b737d-125">**tooadd LCVista from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b737d-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b737d-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b737d-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b737d-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b737d-133">Hello 검색 상자에 입력 **LCVista**합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-133">In hello search box, type **LCVista**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="b737d-135">Hello 결과 패널에서 선택 **LCVista**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-135">In hello results panel, select **LCVista**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b737d-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b737d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b737d-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 LCVista에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b737d-139">Single sign on toowork에 대 한 Azure AD는 tooknow LCVista에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LCVista is tooa user in Azure AD.</span></span> <span data-ttu-id="b737d-140">즉, Azure AD 사용자 및 LCVista에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-140">In other words, a link relationship between an Azure AD user and hello related user in LCVista needs toobe established.</span></span>

<span data-ttu-id="b737d-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** LCVista에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LCVista.</span></span>

<span data-ttu-id="b737d-142">tooconfigure 및 LCVista 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-142">tooconfigure and test Azure AD single sign-on with LCVista, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b737d-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b737d-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b737d-145">**[LCVista 테스트 사용자 만들기](#creating-a-lcvista-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 LCVista에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - toohave a counterpart of Britta Simon in LCVista that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b737d-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b737d-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="b737d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b737d-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b737d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b737d-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 LCVista 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="b737d-150">**tooconfigure Azure AD single sign on, LCVista와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b737d-150">**tooconfigure Azure AD single sign-on with LCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="b737d-151">Hello hello에 Azure 포털에서에서 **LCVista** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-151">In hello Azure portal, on hello **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b737d-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="b737d-155">Hello에 **LCVista 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-155">On hello **LCVista Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="b737d-157">a.</span><span class="sxs-lookup"><span data-stu-id="b737d-157">a.</span></span> <span data-ttu-id="b737d-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="b737d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="b737d-159">b.</span><span class="sxs-lookup"><span data-stu-id="b737d-159">b.</span></span> <span data-ttu-id="b737d-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="b737d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="b737d-161">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-161">These values are not hello real.</span></span> <span data-ttu-id="b737d-162">이러한 항목을 업데이트 실제 hello로 값 식별자 및 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-162">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="b737d-163">연락처 [LCVista 클라이언트 지원 팀](https://lcvista.com/contact) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-163">Contact [LCVista Client support team](https://lcvista.com/contact) tooget these values.</span></span> 

4. <span data-ttu-id="b737d-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="b737d-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="b737d-168">Hello에 **LCVista 구성** 섹션에서 클릭 **구성 LCVista** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="b737d-168">On hello **LCVista Configuration** section, click **Configure LCVista** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b737d-169">복사 hello **SAML 엔터티 ID** 및 **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="b737d-169">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="b737d-171">Tooyour LCVista 응용 프로그램 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-171">Sign on tooyour LCVista application as an administrator.</span></span>

8. <span data-ttu-id="b737d-172">Hello에 **SAML 구성** 섹션에서 hello 확인 **사용 SAML 로그인** 이미지 아래에 설명 된 대로 hello 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-172">In hello **SAML Config** section, check hello **Enable SAML login** and enter hello details as mentioned in below image.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="b737d-174">a.</span><span class="sxs-lookup"><span data-stu-id="b737d-174">a.</span></span> <span data-ttu-id="b737d-175">붙여넣기 hello **발급자 URL** hello에 Azure AD에서 복사한 있는 **엔터티 ID** 섹션.</span><span class="sxs-lookup"><span data-stu-id="b737d-175">Paste hello **Issuer URL** which you have copied from Azure AD in hello **Entity ID** section.</span></span> 

    <span data-ttu-id="b737d-176">b.</span><span class="sxs-lookup"><span data-stu-id="b737d-176">b.</span></span> <span data-ttu-id="b737d-177">붙여넣기 hello **Single Sign-on 서비스 URL** hello에 Azure AD에서 복사한 있는 **URL** 섹션.</span><span class="sxs-lookup"><span data-stu-id="b737d-177">Paste hello **Single Sign-On Service URL** which you have copied from Azure AD in hello **URL** section.</span></span>

    <span data-ttu-id="b737d-178">c.</span><span class="sxs-lookup"><span data-stu-id="b737d-178">c.</span></span> <span data-ttu-id="b737d-179">메타 데이터 (XML)는 Azure 포털에서 다운로드 한 hello 값 복사 **X509Certificate** hello에 붙여 넣을 **x509 인증서** 섹션.</span><span class="sxs-lookup"><span data-stu-id="b737d-179">From Metadata (XML) which you have downloaded from Azure portal, copy hello value **X509Certificate** and paste it in hello **x509 Certificate** section.</span></span>

    <span data-ttu-id="b737d-180">d.</span><span class="sxs-lookup"><span data-stu-id="b737d-180">d.</span></span> <span data-ttu-id="b737d-181">Hello에 **이름 특성** 붙여넣기 hello 값 텍스트 상자 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-181">In hello **First name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="b737d-182">e.</span><span class="sxs-lookup"><span data-stu-id="b737d-182">e.</span></span> <span data-ttu-id="b737d-183">Hello에 **성 특성** 붙여넣기 hello 값 텍스트 상자 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-183">In hello **Last name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="b737d-184">f.</span><span class="sxs-lookup"><span data-stu-id="b737d-184">f.</span></span> <span data-ttu-id="b737d-185">Hello에 **전자 메일 특성** 붙여넣기 hello 값 텍스트 상자 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-185">In hello **Email attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="b737d-186">g.</span><span class="sxs-lookup"><span data-stu-id="b737d-186">g.</span></span> <span data-ttu-id="b737d-187">Hello에 **Username 특성** 붙여넣기 hello 값 텍스트 상자 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-187">In hello **Username attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="b737d-188">e.</span><span class="sxs-lookup"><span data-stu-id="b737d-188">e.</span></span> <span data-ttu-id="b737d-189">클릭 **저장** toosave hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-189">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="b737d-190">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="b737d-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b737d-191">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="b737d-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b737d-192">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b737d-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b737d-193">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b737d-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="b737d-194">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b737d-196">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b737d-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b737d-197">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b737d-199">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b737d-201">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b737d-203">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b737d-205">a.</span><span class="sxs-lookup"><span data-stu-id="b737d-205">a.</span></span> <span data-ttu-id="b737d-206">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b737d-207">b.</span><span class="sxs-lookup"><span data-stu-id="b737d-207">b.</span></span> <span data-ttu-id="b737d-208">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b737d-209">c.</span><span class="sxs-lookup"><span data-stu-id="b737d-209">c.</span></span> <span data-ttu-id="b737d-210">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b737d-211">d.</span><span class="sxs-lookup"><span data-stu-id="b737d-211">d.</span></span> <span data-ttu-id="b737d-212">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="b737d-213">LCVista 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b737d-213">Creating a LCVista test user</span></span>

<span data-ttu-id="b737d-214">이 섹션에서는 LCVista에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="b737d-215">Toocontact 해야 [LCVista 클라이언트 지원 팀](https://lcvista.com/contact) hello LCVista 응용 프로그램의에서 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-215">You need toocontact [LCVista Client support team](https://lcvista.com/contact) tooadd hello users in hello LCVista application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b737d-216">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b737d-217">이 섹션에서는 tooLCVista 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLCVista.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b737d-219">**tooassign Britta Simon tooLCVista hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b737d-219">**tooassign Britta Simon tooLCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="b737d-220">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b737d-222">Hello 응용 프로그램 목록에서 선택 **LCVista**합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-222">In hello applications list, select **LCVista**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="b737d-224">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b737d-226">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-226">Click **Add** button.</span></span> <span data-ttu-id="b737d-227">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b737d-229">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b737d-230">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b737d-231">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b737d-232">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b737d-232">Testing single sign-on</span></span>

<span data-ttu-id="b737d-233">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="b737d-234">Hello LCVista 타일을 클릭 hello 액세스 패널에에서 됩니다 tooOrganization 로그온 페이지 리디렉션.</span><span class="sxs-lookup"><span data-stu-id="b737d-234">Click hello LCVista tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="b737d-235">성공적으로 로그인 한 후 로그온 tooyour LCVista 응용 프로그램 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b737d-235">After successful login, you will be signed-on tooyour LCVista application.</span></span> <span data-ttu-id="b737d-236">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b737d-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b737d-237">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b737d-237">Additional resources</span></span>

* [<span data-ttu-id="b737d-238">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="b737d-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b737d-239">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b737d-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png


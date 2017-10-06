---
title: "자습서: DocuSign과 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 DocuSign 사이의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="214e5-103">자습서: DocuSign와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="214e5-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="214e5-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 DocuSign 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-104">In this tutorial, you learn how toointegrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="214e5-105">Azure AD와 DocuSign 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-105">Integrating DocuSign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="214e5-106">액세스 tooDocuSign을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-106">You can control in Azure AD who has access tooDocuSign</span></span>
- <span data-ttu-id="214e5-107">프로그램 사용자 tooautomatically get 로그온 tooDocuSign (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-107">You can enable your users tooautomatically get signed-on tooDocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="214e5-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="214e5-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="214e5-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="214e5-110">Prerequisites</span></span>

<span data-ttu-id="214e5-111">Azure AD 및 DocuSign 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-111">tooconfigure Azure AD integration with DocuSign, you need hello following items:</span></span>

- <span data-ttu-id="214e5-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="214e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="214e5-113">DocuSign Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="214e5-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="214e5-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="214e5-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="214e5-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="214e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="214e5-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="214e5-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="214e5-118">Scenario description</span></span>
<span data-ttu-id="214e5-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="214e5-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="214e5-121">DocuSign은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="214e5-121">Adding DocuSign from hello gallery</span></span>
2. <span data-ttu-id="214e5-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="214e5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-hello-gallery"></a><span data-ttu-id="214e5-123">DocuSign은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="214e5-123">Adding DocuSign from hello gallery</span></span>
<span data-ttu-id="214e5-124">tooconfigure hello와의 통합 DocuSign Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 DocuSign tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-124">tooconfigure hello integration of DocuSign into Azure AD, you need tooadd DocuSign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="214e5-125">**hello 갤러리에서 DocuSign tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="214e5-125">**tooadd DocuSign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="214e5-126">Hello에 ** [Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="214e5-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="214e5-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="214e5-131">클릭 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="214e5-133">Hello 검색 상자에 입력 **DocuSign**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-133">In hello search box, type **DocuSign**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="214e5-135">Hello 결과 패널에서 선택 **DocuSign**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-135">In hello results panel, select **DocuSign**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="214e5-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="214e5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="214e5-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 DocuSign에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="214e5-139">Single sign on toowork에 대 한 Azure AD는 tooknow DocuSign에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DocuSign is tooa user in Azure AD.</span></span> <span data-ttu-id="214e5-140">즉, Azure AD 사용자 및 DocuSign의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-140">In other words, a link relationship between an Azure AD user and hello related user in DocuSign needs toobe established.</span></span>

<span data-ttu-id="214e5-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** DocuSign에 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in DocuSign.</span></span>

<span data-ttu-id="214e5-142">tooconfigure 및 DocuSign 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-142">tooconfigure and test Azure AD single sign-on with DocuSign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="214e5-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on) ** -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="214e5-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="214e5-145">**[DocuSign 테스트 사용자 만들기](#creating-a-docusign-test-user) ** -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 DocuSign에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - toohave a counterpart of Britta Simon in DocuSign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="214e5-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="214e5-147">**[Single Sign-on 테스트](#testing-single-sign-on) ** -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="214e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="214e5-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="214e5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="214e5-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 DocuSign 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="214e5-150">**Azure AD tooconfigure single sign on 및 docusign, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="214e5-150">**tooconfigure Azure AD single sign-on with DocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="214e5-151">Hello hello에 Azure 포털에서에서 **DocuSign** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-151">In hello Azure portal, on hello **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="214e5-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="214e5-155">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (base-64)** 한 다음 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-155">On hello **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="214e5-157">Hello에 **DocuSign 구성** 클릭 하 여 Azure 포털의 섹션 **구성 DocuSign** sign on 구성 tooopen 창.</span><span class="sxs-lookup"><span data-stu-id="214e5-157">On hello **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** tooopen Configure sign-on window.</span></span> <span data-ttu-id="214e5-158">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="214e5-158">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="214e5-160">로그인 tooyour 다른 웹 브라우저 창에서 **DocuSign 관리자 포털** 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-160">In a different web browser window, login tooyour **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="214e5-161">Hello hello 왼쪽 탐색 메뉴를 클릭 **도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-161">In hello navigation menu on hello left, click **Domains**.</span></span>
   
    ![Single Sign-On 구성][51]

7. <span data-ttu-id="214e5-163">Hello 오른쪽 창에서 클릭 **클레임 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-163">On hello right pane, click **Claim Domain**.</span></span>
   
    ![Single Sign-On 구성][52]

8. <span data-ttu-id="214e5-165">Hello에 **도메인 클레임** 대화 상자에서 hello **도메인 이름** 텍스트 상자에 회사 도메인을 입력 한 다음 클릭 **클레임**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-165">On hello **Claim a domain** dialog, in hello **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="214e5-166">Hello 도메인을 확인 하 고 hello 상태 활성화 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-166">Make sure that you verify hello domain and hello status is active.</span></span>
   
    ![Single Sign-On 구성][53]

9. <span data-ttu-id="214e5-168">Hello 왼쪽 메뉴에서 **Id 공급자**</span><span class="sxs-lookup"><span data-stu-id="214e5-168">In menu on hello left side, click **Identity Providers**</span></span>  
   
    ![Single Sign-On 구성][54]
10. <span data-ttu-id="214e5-170">Hello 오른쪽 창에서 클릭 **Id 공급자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-170">In hello right pane, click **Add Identity Provider**.</span></span> 
   
    ![Single Sign-On 구성][55]

11. <span data-ttu-id="214e5-172">Hello에 **Id 공급자 설정** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-172">On hello **Identity Provider Settings** page, perform hello following steps:</span></span>
   
    ![Single Sign-On 구성][56]

    <span data-ttu-id="214e5-174">a.</span><span class="sxs-lookup"><span data-stu-id="214e5-174">a.</span></span> <span data-ttu-id="214e5-175">Hello에 **이름** textbox 구성에 대 한 고유한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-175">In hello **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="214e5-176">공백을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="214e5-176">Do not use spaces.</span></span>

    <span data-ttu-id="214e5-177">b.</span><span class="sxs-lookup"><span data-stu-id="214e5-177">b.</span></span> <span data-ttu-id="214e5-178">붙여넣기 **SAML 엔터티 ID** hello에 **Id 공급자 발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-178">Paste **SAML Entity ID** into hello **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="214e5-179">c.</span><span class="sxs-lookup"><span data-stu-id="214e5-179">c.</span></span> <span data-ttu-id="214e5-180">붙여넣기 **SAML Single Sign-on 서비스 URL** hello에 **Id 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-180">Paste **SAML Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="214e5-181">d.</span><span class="sxs-lookup"><span data-stu-id="214e5-181">d.</span></span> <span data-ttu-id="214e5-182">붙여넣기 **Sign-Out URL** hello에 **Identity Provider Logout URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-182">Paste **Sign-Out URL** into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="214e5-183">e.</span><span class="sxs-lookup"><span data-stu-id="214e5-183">e.</span></span> <span data-ttu-id="214e5-184">**Sign AuthN 요청**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="214e5-185">f.</span><span class="sxs-lookup"><span data-stu-id="214e5-185">f.</span></span> <span data-ttu-id="214e5-186">**AuthN 요청 보내기**로 **POST**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="214e5-187">g.</span><span class="sxs-lookup"><span data-stu-id="214e5-187">g.</span></span> <span data-ttu-id="214e5-188">**로그아웃 요청 보내기**로 **GET**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="214e5-189">Hello에 **사용자 지정 특성 매핑** 섹션에서 hello 필드를 선택 된 Azure AD 클레임이 toomap 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-189">In hello **Custom Attribute Mapping** section, choose hello field you want toomap with Azure AD Claim.</span></span> <span data-ttu-id="214e5-190">이 예제에서는 hello **emailaddress** 클레임 hello 값이 매핑된 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-190">In this example, hello **emailaddress** claim is mapped with hello value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="214e5-191">전자 메일 클레임에 대 한 Azure AD에서 hello 기본 클레임 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-191">It is hello default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="214e5-192">적절 한 사용 하 여 hello **사용자 식별자** Azure AD tooDocuSign 사용자 매핑에서 toomap hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-192">Use hello appropriate **User identifier** toomap hello user from Azure AD tooDocuSign user mapping.</span></span> <span data-ttu-id="214e5-193">선택 hello 적절 한 필드 및 조직 설정에 따라 hello 적절 한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-193">Select hello proper Field and enter hello appropriate value based on your organization settings.</span></span>
          
    ![Single Sign-On 구성][57]

13. <span data-ttu-id="214e5-195">Hello에 **Id 공급자 인증서** 섹션에서 클릭 **인증서 추가**, 한 다음 Azure AD 포털에서 다운로드 한 hello 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-195">In hello **Identity Provider Certificate** section, click **Add Certificate**, and then upload hello certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Single Sign-On 구성][58]

14. <span data-ttu-id="214e5-197">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-197">Click **Save**.</span></span>

15. <span data-ttu-id="214e5-198">Hello에 **Id 공급자** 섹션에서 클릭 **동작**, 클릭 하 고 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-198">In hello **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Single Sign-On 구성][59]
 
16. <span data-ttu-id="214e5-200">Hello에 **SAML 2.0 끝점 보기** 섹션에서 **DocuSign 관리자 포털**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-200">In hello **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform hello following steps:</span></span>
   
    ![Single Sign-On 구성][60]
   
    <span data-ttu-id="214e5-202">a.</span><span class="sxs-lookup"><span data-stu-id="214e5-202">a.</span></span> <span data-ttu-id="214e5-203">복사 hello **서비스 공급자 발급자 URL**, hello에 붙여 **식별자** 텍스트 상자에 **DocuSign 도메인 및 Url** hello Azure 포털 다음 hello의 섹션 패턴: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-203">Copy hello **Service Provider Issuer URL**, and then paste into hello **Identifier** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="214e5-204">b.</span><span class="sxs-lookup"><span data-stu-id="214e5-204">b.</span></span> <span data-ttu-id="214e5-205">복사 hello **서비스 공급자 로그인 URL**, hello에 붙여 **로그온 URL** 텍스트 상자에 **DocuSign 도메인 및 Url** hello Azure 포털 다음 hello의 섹션 패턴: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-205">Copy hello **Service Provider Login URL**, and then paste into hello **Sign On URL** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="214e5-207">c.</span><span class="sxs-lookup"><span data-stu-id="214e5-207">c.</span></span>  <span data-ttu-id="214e5-208">페이지 맨 아래에 있는 **닫기**</span><span class="sxs-lookup"><span data-stu-id="214e5-208">Click **Close**</span></span>
    
17. <span data-ttu-id="214e5-209">Hello Azure 포털에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-209">On hello Azure portal, click **Save**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="214e5-211">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="214e5-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="214e5-212">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서 ** 구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="214e5-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="214e5-213">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="214e5-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="214e5-214">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="214e5-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="214e5-215">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="214e5-217">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="214e5-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="214e5-218">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="214e5-220">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="214e5-222">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="214e5-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="214e5-224">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="214e5-226">a.</span><span class="sxs-lookup"><span data-stu-id="214e5-226">a.</span></span> <span data-ttu-id="214e5-227">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="214e5-228">b.</span><span class="sxs-lookup"><span data-stu-id="214e5-228">b.</span></span> <span data-ttu-id="214e5-229">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="214e5-230">c.</span><span class="sxs-lookup"><span data-stu-id="214e5-230">c.</span></span> <span data-ttu-id="214e5-231">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="214e5-232">d.</span><span class="sxs-lookup"><span data-stu-id="214e5-232">d.</span></span> <span data-ttu-id="214e5-233">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="214e5-234">DocuSign 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="214e5-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="214e5-235">응용 프로그램이 지 원하는 **적시 사용자 프로 비전 하기만** 전후의 인증 사용자 hello 응용 프로그램에서 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-235">Application supports **Just in time user provisioning** and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="214e5-236">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="214e5-237">이 섹션에서는 액세스 tooDocuSign 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooDocuSign.</span></span>

![사용자 할당][200] 

<span data-ttu-id="214e5-239">**tooassign Britta Simon tooDocuSign hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="214e5-239">**tooassign Britta Simon tooDocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="214e5-240">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="214e5-242">Hello 응용 프로그램 목록에서 선택 **DocuSign**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-242">In hello applications list, select **DocuSign**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="214e5-244">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="214e5-246">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-246">Click **Add** button.</span></span> <span data-ttu-id="214e5-247">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="214e5-249">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="214e5-250">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="214e5-251">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="214e5-252">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="214e5-252">Testing single sign-on</span></span>

<span data-ttu-id="214e5-253">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="214e5-254">Hello 액세스 패널에서에서 hello DocuSign 타일을 클릭할 때 자동으로 로그온 tooyour DocuSign 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-254">When you click hello DocuSign tile in hello Access Panel, you should get automatically signed-on tooyour DocuSign application.</span></span>
<span data-ttu-id="214e5-255">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="214e5-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="214e5-256">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="214e5-256">Additional resources</span></span>

* [<span data-ttu-id="214e5-257">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="214e5-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="214e5-258">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="214e5-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="214e5-259">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="214e5-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png


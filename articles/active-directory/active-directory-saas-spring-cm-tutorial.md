---
title: "자습서: SpringCM과 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 SpringCM 간에 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="20052-103">자습서: SpringCM과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="20052-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="20052-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 SpringCM 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-104">In this tutorial, you learn how toointegrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="20052-105">다음 이점을 hello로 제공 SpringCM Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="20052-105">Integrating SpringCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="20052-106">액세스 tooSpringCM을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20052-106">You can control in Azure AD who has access tooSpringCM</span></span>
- <span data-ttu-id="20052-107">프로그램 사용자 tooautomatically get 로그온 tooSpringCM (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20052-107">You can enable your users tooautomatically get signed-on tooSpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="20052-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20052-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="20052-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20052-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="20052-110">Prerequisites</span></span>

<span data-ttu-id="20052-111">SpringCM와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-111">tooconfigure Azure AD integration with SpringCM, you need hello following items:</span></span>

- <span data-ttu-id="20052-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="20052-112">An Azure AD subscription</span></span>
- <span data-ttu-id="20052-113">SpringCM Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="20052-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="20052-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="20052-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="20052-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="20052-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="20052-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20052-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="20052-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="20052-118">Scenario description</span></span>
<span data-ttu-id="20052-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="20052-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20052-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="20052-121">SpringCM은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="20052-121">Adding SpringCM from hello gallery</span></span>
2. <span data-ttu-id="20052-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="20052-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-hello-gallery"></a><span data-ttu-id="20052-123">SpringCM은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="20052-123">Adding SpringCM from hello gallery</span></span>
<span data-ttu-id="20052-124">tooconfigure hello와의 통합 SpringCM Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SpringCM tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-124">tooconfigure hello integration of SpringCM into Azure AD, you need tooadd SpringCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="20052-125">**SpringCM hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="20052-125">**tooadd SpringCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="20052-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="20052-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="20052-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="20052-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="20052-133">Hello 검색 상자에 입력 **SpringCM**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-133">In hello search box, type **SpringCM**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="20052-135">Hello 결과 패널에서 선택 **SpringCM**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-135">In hello results panel, select **SpringCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="20052-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="20052-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="20052-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SpringCM에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="20052-139">Single sign on toowork에 대 한 Azure AD는 tooknow SpringCM에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SpringCM is tooa user in Azure AD.</span></span> <span data-ttu-id="20052-140">즉, Azure AD 사용자와 SpringCM에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-140">In other words, a link relationship between an Azure AD user and hello related user in SpringCM needs toobe established.</span></span>

<span data-ttu-id="20052-141">SpringCM에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-141">In SpringCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="20052-142">tooconfigure 및 SpringCM 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-142">tooconfigure and test Azure AD single sign-on with SpringCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="20052-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="20052-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="20052-145">**[SpringCM 테스트 사용자 만들기](#creating-a-springcm-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 SpringCM에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - toohave a counterpart of Britta Simon in SpringCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="20052-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="20052-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="20052-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="20052-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="20052-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="20052-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 SpringCM 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="20052-150">**tooconfigure Azure AD single sign on SpringCM와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="20052-150">**tooconfigure Azure AD single sign-on with SpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="20052-151">Hello hello에 Azure 포털에서에서 **SpringCM** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-151">In hello Azure portal, on hello **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="20052-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="20052-155">Hello에 **SpringCM 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-155">On hello **SpringCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="20052-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="20052-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="20052-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="20052-158">This value is not real.</span></span> <span data-ttu-id="20052-159">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="20052-160">연락처 [SpringCM 클라이언트 지원 팀](https://knowledge.springcm.com/support) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="20052-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Raw)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="20052-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="20052-165">Hello에 **SpringCM 구성** 섹션에서 클릭 **구성 SpringCM** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="20052-165">On hello **SpringCM Configuration** section, click **Configure SpringCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="20052-166">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="20052-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="20052-168">다른 웹 브라우저 창에서 tooyour 로그인 **SpringCM** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-168">In a different web browser window, sign on tooyour **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="20052-169">Hello 메뉴에서 hello 위에 표시를 클릭 **이동**, 클릭 **기본 설정**를 선택한 다음 hello **계정 기본 설정** 섹션에서 클릭 **SAML SSO**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-169">In hello menu on hello top, click **GO TO**, click **Preferences**, and then, in hello **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="20052-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span><span class="sxs-lookup"><span data-stu-id="20052-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="20052-171">Hello Id 공급자 구성 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-171">In hello Identity Provider Configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="20052-172">![ID 공급자 구성](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "ID 공급자 구성")</span><span class="sxs-lookup"><span data-stu-id="20052-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="20052-173">a.</span><span class="sxs-lookup"><span data-stu-id="20052-173">a.</span></span> <span data-ttu-id="20052-174">tooupload 다운로드 한 Azure Active Directory 인증서를 클릭 하 여 **인증서 선택** 또는 **발급자 인증서 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-174">tooupload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="20052-175">b.</span><span class="sxs-lookup"><span data-stu-id="20052-175">b.</span></span> <span data-ttu-id="20052-176">붙여넣기 **SAML 엔터티 ID** hello에 Azure 포털에서 복사한 값 **발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="20052-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into hello **Issuer** textbox.</span></span>
    
    <span data-ttu-id="20052-177">c.</span><span class="sxs-lookup"><span data-stu-id="20052-177">c.</span></span> <span data-ttu-id="20052-178">붙여넣기 **SAML Single Sign-on 서비스 URL** hello에 hello Azure 포털에서에서 복사한 값 **서비스 공급자 (SP) 시작 끝점** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="20052-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="20052-179">d.</span><span class="sxs-lookup"><span data-stu-id="20052-179">d.</span></span> <span data-ttu-id="20052-180">**사용**으로 **SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="20052-181">e.</span><span class="sxs-lookup"><span data-stu-id="20052-181">e.</span></span> <span data-ttu-id="20052-182">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="20052-183">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="20052-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="20052-184">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="20052-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="20052-185">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="20052-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="20052-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="20052-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="20052-187">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="20052-189">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="20052-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="20052-190">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="20052-192">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="20052-194">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="20052-196">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="20052-198">a.</span><span class="sxs-lookup"><span data-stu-id="20052-198">a.</span></span> <span data-ttu-id="20052-199">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="20052-200">b.</span><span class="sxs-lookup"><span data-stu-id="20052-200">b.</span></span> <span data-ttu-id="20052-201">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="20052-202">c.</span><span class="sxs-lookup"><span data-stu-id="20052-202">c.</span></span> <span data-ttu-id="20052-203">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="20052-204">d.</span><span class="sxs-lookup"><span data-stu-id="20052-204">d.</span></span> <span data-ttu-id="20052-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="20052-206">SpringCM 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="20052-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="20052-207">Azure Active Directory 사용자 toolog tooenable tooSpringCM에서 프로 비전 해야 SpringCM에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20052-207">tooenable Azure Active Directory users toolog in tooSpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="20052-208">Hello SpringCM의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-208">In hello case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="20052-209">자세한 내용은 [SpringCM 사용자 만들기 및 편집](http://knowledge.springcm.com/create-and-edit-a-springcm-user)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20052-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="20052-210">**사용자 계정 tooSpringCM tooprovision hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="20052-210">**tooprovision a user account tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="20052-211">Tooyour 로그인 **SpringCM** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-211">Log in tooyour **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="20052-212">**GOTO**를 클릭하고 **주소록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="20052-213">![사용자 만들기](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="20052-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="20052-214">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-214">Click **Create User**.</span></span>

4. <span data-ttu-id="20052-215">**사용자 역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="20052-216">**활성화 메일 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="20052-217">형식 hello 첫 번째 이름, 성, 이름 및 tooprovision hello에 하려는 유효한 Azure Active Directory 사용자 계정의 전자 메일 주소 관련 텍스트 상자.</span><span class="sxs-lookup"><span data-stu-id="20052-217">Type hello first name, last name, and email address of a valid Azure Active Directory user account you want tooprovision into hello related textboxes.</span></span>

7. <span data-ttu-id="20052-218">Hello 사용자 tooa 추가 **보안 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-218">Add hello user tooa **Security group**.</span></span>

8. <span data-ttu-id="20052-219">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="20052-220">다른 SpringCM 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision SpringCM에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="20052-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM tooprovision AAD user accounts.</span></span>  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="20052-221">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="20052-222">이 섹션에서는 tooSpringCM 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringCM.</span></span>

![사용자 할당][200] 

<span data-ttu-id="20052-224">**tooassign Britta Simon tooSpringCM hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="20052-224">**tooassign Britta Simon tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="20052-225">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="20052-227">Hello 응용 프로그램 목록에서 선택 **SpringCM**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-227">In hello applications list, select **SpringCM**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="20052-229">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="20052-231">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-231">Click **Add** button.</span></span> <span data-ttu-id="20052-232">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="20052-234">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20052-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="20052-235">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="20052-236">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="20052-237">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="20052-237">Testing single sign-on</span></span>

<span data-ttu-id="20052-238">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20052-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="20052-239">Hello 액세스 패널에서에서 hello SpringCM 타일을 클릭할 때 자동으로 로그온 tooyour SpringCM 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-239">When you click hello SpringCM tile in hello Access Panel, you should get automatically signed-on tooyour SpringCM application.</span></span>

<span data-ttu-id="20052-240">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="20052-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="20052-241">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="20052-241">Additional resources</span></span>

* [<span data-ttu-id="20052-242">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="20052-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="20052-243">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="20052-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png


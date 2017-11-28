---
title: "자습서: Pingboard와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Pingboard 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="b5b24-103">자습서: Pingboard와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b5b24-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="b5b24-104">이 자습서에 설명 어떻게 toointegrate Pingboard Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b5b24-104">In this tutorial, you learn how toointegrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5b24-105">다음 이점을 hello로 제공 Pingboard Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="b5b24-105">Integrating Pingboard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b5b24-106">액세스 tooPingboard을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-106">You can control in Azure AD who has access tooPingboard</span></span>
- <span data-ttu-id="b5b24-107">프로그램 사용자 tooautomatically get 로그온 tooPingboard (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-107">You can enable your users tooautomatically get signed-on tooPingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b5b24-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="b5b24-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5b24-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b5b24-110">Prerequisites</span></span>

<span data-ttu-id="b5b24-111">다음 항목 hello가 필요 tooconfigure Pingboard와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-111">tooconfigure Azure AD integration with Pingboard, you need hello following items:</span></span>

- <span data-ttu-id="b5b24-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b5b24-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5b24-113">Pingboard Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b5b24-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5b24-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5b24-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5b24-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b5b24-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5b24-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b5b24-118">Scenario description</span></span>
<span data-ttu-id="b5b24-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5b24-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5b24-121">Pingboard는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b5b24-121">Adding Pingboard from hello gallery</span></span>
2. <span data-ttu-id="b5b24-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b5b24-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-hello-gallery"></a><span data-ttu-id="b5b24-123">Pingboard는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b5b24-123">Adding Pingboard from hello gallery</span></span>
<span data-ttu-id="b5b24-124">tooconfigure hello와의 통합 Pingboard Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Pingboard tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-124">tooconfigure hello integration of Pingboard into Azure AD, you need tooadd Pingboard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b5b24-125">**hello 갤러리에서 Pingboard tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5b24-125">**tooadd Pingboard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5b24-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5b24-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b5b24-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b5b24-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b5b24-133">Hello 검색 상자에 입력 **Pingboard**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-133">In hello search box, type **Pingboard**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="b5b24-135">Hello 결과 패널에서 선택 **Pingboard**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-135">In hello results panel, select **Pingboard**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b5b24-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b5b24-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b5b24-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Pingboard에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b5b24-139">Single sign on toowork에 대 한 Azure AD는 tooknow Pingboard에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pingboard is tooa user in Azure AD.</span></span> <span data-ttu-id="b5b24-140">즉, Azure AD 사용자 및 Pingboard에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-140">In other words, a link relationship between an Azure AD user and hello related user in Pingboard needs toobe established.</span></span>

<span data-ttu-id="b5b24-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Pingboard에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Pingboard.</span></span>

<span data-ttu-id="b5b24-142">tooconfigure 및 Pingboard 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-142">tooconfigure and test Azure AD single sign-on with Pingboard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b5b24-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b5b24-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5b24-145">**[Pingboard 테스트 사용자 만들기](#creating-a-pingboard-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Pingboard에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - toohave a counterpart of Britta Simon in Pingboard that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="b5b24-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5b24-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="b5b24-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b5b24-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b5b24-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b5b24-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 Pingboard 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="b5b24-150">**tooconfigure Azure AD single sign on, Pingboard와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5b24-150">**tooconfigure Azure AD single sign-on with Pingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5b24-151">Hello에 hello Azure 관리 포털에서 **Pingboard** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-151">In hello Azure Management portal, on hello **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b5b24-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="b5b24-155">Hello에 **Pingboard 도메인 및 Url** 섹션를 hello tooconfigure hello 응용 프로그램에 필요한 경우 다음 단계를 수행 **IDP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="b5b24-155">On hello **Pingboard Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="b5b24-157">a.</span><span class="sxs-lookup"><span data-stu-id="b5b24-157">a.</span></span> <span data-ttu-id="b5b24-158">Hello에 **식별자** 형식 hello 값으로 텍스트 상자:`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="b5b24-158">In hello **Identifier** textbox, type hello value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="b5b24-159">b.</span><span class="sxs-lookup"><span data-stu-id="b5b24-159">b.</span></span> <span data-ttu-id="b5b24-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="b5b24-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b5b24-161">이러한 없는지 hello 실제 값 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b5b24-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="b5b24-162">Tooupdate hello 실제 식별자와 회신 URL 사용 하 여 이러한 값 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="b5b24-163">여기 있습니다 toouse hello의 고유 값을 hello 식별자의에서 문자열을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="b5b24-164">연락처 [Pingboard 클라이언트 지원 팀](https://support.pingboard.com/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-164">Contact [Pingboard Client support team](https://support.pingboard.com/) tooget these values.</span></span> 

4. <span data-ttu-id="b5b24-165">확인 **고급 URL 설정 표시**tooconfigure hello 응용 프로그램에 필요한 경우, **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="b5b24-165">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="b5b24-167">a.</span><span class="sxs-lookup"><span data-stu-id="b5b24-167">a.</span></span> <span data-ttu-id="b5b24-168">Hello에 **로그온 URL** 형식 hello 값으로 텍스트 상자:`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="b5b24-168">In hello **Sign-on URL** textbox, type hello value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="b5b24-169">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="b5b24-171">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-171">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b5b24-173">Pingboard 측에서는 SSO tooconfigure 새 브라우저 창을 열고 tooyour Pingboard 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-173">tooconfigure SSO on Pingboard side, open a new browser window and log in tooyour Pingboard Account.</span></span> <span data-ttu-id="b5b24-174">단일 기호를 Pingboard admin tooset에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-174">You must be a Pingboard admin tooset up single sign on.</span></span>

8. <span data-ttu-id="b5b24-175">Hello 상단 메뉴에서 선택 **앱 > 통합**</span><span class="sxs-lookup"><span data-stu-id="b5b24-175">From hello top menu select **Apps > Integrations**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="b5b24-177">Hello에 **통합** 페이지, hello **"Azure Active Directory"** 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-177">On hello **Integrations** page, find hello **"Azure Active Directory"** tile, and click it.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="b5b24-179">클릭 하 여 다음에 나오는 모달 hello에 **"구성"**</span><span class="sxs-lookup"><span data-stu-id="b5b24-179">In hello modal that follows click **"Configure"**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="b5b24-181">다음 페이지 hello에 "Azure SSO 통합 사용 됩니다." 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-181">On hello following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="b5b24-182">열기 hello에 콘텐츠 메모장 및 붙여넣기 hello에 메타 데이터 XML 파일을 다운로드 한 **IDP 메타 데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-182">Open hello downloaded Metadata XML file in a notepad and paste hello content in **IDP Metadata**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="b5b24-184">hello 파일 유효성을 검사할 및 single sign-on 사용 이제 모든 항목이 올바르면</span><span class="sxs-lookup"><span data-stu-id="b5b24-184">hello file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b5b24-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b5b24-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="b5b24-186">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-186">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b5b24-188">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5b24-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5b24-189">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-189">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5b24-191">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5b24-193">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="b5b24-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5b24-195">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5b24-197">a.</span><span class="sxs-lookup"><span data-stu-id="b5b24-197">a.</span></span> <span data-ttu-id="b5b24-198">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5b24-199">b.</span><span class="sxs-lookup"><span data-stu-id="b5b24-199">b.</span></span> <span data-ttu-id="b5b24-200">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b5b24-201">c.</span><span class="sxs-lookup"><span data-stu-id="b5b24-201">c.</span></span> <span data-ttu-id="b5b24-202">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b5b24-203">d.</span><span class="sxs-lookup"><span data-stu-id="b5b24-203">d.</span></span> <span data-ttu-id="b5b24-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="b5b24-205">Pingboard 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b5b24-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="b5b24-206">Tooenable Azure AD 사용자가 toolog Pingboard로 주문 하 고에 Pingboard에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-206">In order tooenable Azure AD users toolog into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="b5b24-207">Hello Pingboard의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-207">In hello case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="b5b24-208">**사용자 계정 수행 tooprovision hello 다음 단계:**</span><span class="sxs-lookup"><span data-stu-id="b5b24-208">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5b24-209">관리자 권한으로 Pingboard 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-209">Log in tooyour Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="b5b24-210">**디렉터리** 페이지에서 **"직원 추가"** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![직원 추가](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="b5b24-212">Hello에 **"직원 추가"** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-212">On hello **“Add Employee”** dialog page, perform hello following steps.</span></span>

    ![피플 초대](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="b5b24-214">a.</span><span class="sxs-lookup"><span data-stu-id="b5b24-214">a.</span></span> <span data-ttu-id="b5b24-215">Hello에 **전체 이름을** 텍스트 형식 hello Britta Simon의 전체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-215">In hello **Full Name** textbox, type hello full name of Britta Simon.</span></span>

    <span data-ttu-id="b5b24-216">b.</span><span class="sxs-lookup"><span data-stu-id="b5b24-216">b.</span></span> <span data-ttu-id="b5b24-217">Hello에 **전자 메일** textbox Britta Simon 계정의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-217">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="b5b24-218">c.</span><span class="sxs-lookup"><span data-stu-id="b5b24-218">c.</span></span> <span data-ttu-id="b5b24-219">Hello에 **직함** textbox Britta Simon의 hello 작업 제목을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-219">In hello **Job Title** textbox, type hello job title of Britta Simon.</span></span>

    <span data-ttu-id="b5b24-220">d.</span><span class="sxs-lookup"><span data-stu-id="b5b24-220">d.</span></span> <span data-ttu-id="b5b24-221">Hello에 **위치** 드롭다운에서 Britta Simon의 선택 hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-221">In hello **Location** dropdown, select hello location  of Britta Simon.</span></span>
    
    <span data-ttu-id="b5b24-222">e.</span><span class="sxs-lookup"><span data-stu-id="b5b24-222">e.</span></span> <span data-ttu-id="b5b24-223">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-223">Click **Add**.</span></span>   

4. <span data-ttu-id="b5b24-224">확인 화면 tooconfirm hello 추가 사용자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-224">A confirmation screen will come up tooconfirm hello addition of user.</span></span>
    
    ![확인](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="b5b24-226">hello Azure Active Directory 계정 소유자 전자 메일을 받게 되 고 링크 tooconfirm 자신의 계정을 활성화 되기 전에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-226">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b5b24-227">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b5b24-228">이 섹션에서는 액세스 tooPingboard 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPingboard.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b5b24-230">**tooassign Britta Simon tooPingboard hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5b24-230">**tooassign Britta Simon tooPingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5b24-231">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-231">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b5b24-233">Hello 응용 프로그램 목록에서 선택 **Pingboard**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-233">In hello applications list, select **Pingboard**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="b5b24-235">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b5b24-237">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-237">Click **Add** button.</span></span> <span data-ttu-id="b5b24-238">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b5b24-240">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b5b24-241">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5b24-242">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b5b24-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b5b24-243">Testing single sign-on</span></span>

<span data-ttu-id="b5b24-244">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b5b24-245">Hello 액세스 패널에서에서 hello Pingboard 타일을 클릭할 때 자동으로 로그온 tooyour Pingboard 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b24-245">When you click hello Pingboard tile in hello Access Panel, you should get automatically signed-on tooyour Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b5b24-246">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b5b24-246">Additional resources</span></span>

* [<span data-ttu-id="b5b24-247">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="b5b24-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5b24-248">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b5b24-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png

---
title: "자습서: GitHub와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 GitHub 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="956c5-103">자습서: GitHub와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="956c5-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="956c5-104">이 자습서에 설명 어떻게 toointegrate GitHub Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="956c5-104">In this tutorial, you learn how toointegrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="956c5-105">GitHub Azure AD와 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-105">Integrating GitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="956c5-106">액세스 tooGitHub을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-106">You can control in Azure AD who has access tooGitHub</span></span>
- <span data-ttu-id="956c5-107">프로그램 사용자 tooautomatically get 로그온 tooGitHub (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-107">You can enable your users tooautomatically get signed-on tooGitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="956c5-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="956c5-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="956c5-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="956c5-110">Prerequisites</span></span>

<span data-ttu-id="956c5-111">GitHub와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-111">tooconfigure Azure AD integration with GitHub, you need hello following items:</span></span>

- <span data-ttu-id="956c5-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="956c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="956c5-113">GitHub Single Sign-On을 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="956c5-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="956c5-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="956c5-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="956c5-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="956c5-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="956c5-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="956c5-118">Scenario description</span></span>
<span data-ttu-id="956c5-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="956c5-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="956c5-121">GitHub은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="956c5-121">Adding GitHub from hello gallery</span></span>
2. <span data-ttu-id="956c5-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="956c5-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-hello-gallery"></a><span data-ttu-id="956c5-123">GitHub은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="956c5-123">Adding GitHub from hello gallery</span></span>
<span data-ttu-id="956c5-124">tooconfigure hello 통합 GitHub의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 GitHub tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-124">tooconfigure hello integration of GitHub into Azure AD, you need tooadd GitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="956c5-125">**hello 갤러리에서 GitHub tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="956c5-125">**tooadd GitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="956c5-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="956c5-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="956c5-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="956c5-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="956c5-133">Hello 검색 상자에 입력 **GitHub.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-133">In hello search box, type **GitHub.com**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="956c5-135">Hello 결과 패널에서 선택 **GitHub**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-135">In hello results panel, select **GitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="956c5-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="956c5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="956c5-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 GitHub에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="956c5-139">Single sign on toowork에 대 한 Azure AD는 tooknow GitHub에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="956c5-140">즉, Azure AD 사용자 및 GitHub의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-140">In other words, a link relationship between an Azure AD user and hello related user in GitHub needs toobe established.</span></span>

<span data-ttu-id="956c5-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in GitHub.</span></span>

<span data-ttu-id="956c5-142">tooconfigure 및 GitHub 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-142">tooconfigure and test Azure AD single sign-on with GitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="956c5-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="956c5-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="956c5-145">**[GitHub 테스트 사용자 만들기](#creating-a-GitHub-test-user)**  -toohave 표현인 연결 된 Azure AD toohello 그녀는 GitHub에서 Britta Simon의 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - toohave a counterpart of Britta Simon in GitHub that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="956c5-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="956c5-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="956c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="956c5-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="956c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="956c5-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 GitHub 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="956c5-150">**tooconfigure Azure AD single sign on GitHub와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="956c5-150">**tooconfigure Azure AD single sign-on with GitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="956c5-151">Hello에 hello Azure 관리 포털에서 **GitHub** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-151">In hello Azure Management portal, on hello **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="956c5-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="956c5-155">Hello에 **GitHub 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-155">On hello **GitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="956c5-157">a.</span><span class="sxs-lookup"><span data-stu-id="956c5-157">a.</span></span> <span data-ttu-id="956c5-158">Hello에 **로그온 URL** 형식 hello 값으로 텍스트 상자:`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="956c5-158">In hello **Sign-on URL** textbox, type hello value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="956c5-159">b.</span><span class="sxs-lookup"><span data-stu-id="956c5-159">b.</span></span> <span data-ttu-id="956c5-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="956c5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="956c5-161">이러한 없는지 hello 실제 값 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="956c5-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="956c5-162">Tooupdate hello 실제 사인에 URL과 식별자를 사용 하 여 이러한 값 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-162">You have tooupdate these values with hello actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="956c5-163">여기 있습니다 toouse hello의 고유 값을 hello 식별자의에서 문자열을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="956c5-164">TooGitHub 관리자 섹션 tooretrieve 이러한 값을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-164">Go tooGitHub Admin section tooretrieve these values.</span></span> 

4. <span data-ttu-id="956c5-165">Hello에 **사용자 특성** 섹션에서 **사용자 식별자** user.mail으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-165">On hello **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="956c5-167">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **새 인증서 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-167">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="956c5-169">Hello에 **새 인증서 만들기** 대화 상자에서 hello 달력 아이콘을 클릭 하 고 선택 된 **만료 날짜**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-169">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="956c5-170">그런 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-170">Then click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="956c5-172">Hello에 **SAML 서명 인증서** 섹션에서 **새 인증서를 활성화할** 클릭 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-172">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="956c5-174">Hello 팝업에서 **롤오버 인증서** 창 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-174">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="956c5-176">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-176">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="956c5-178">Hello에 **GitHub 구성** 섹션에서 클릭 **GitHub 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="956c5-178">On hello **GitHub Configuration** section, click **Configure GitHub** tooopen **Configure sign-on** window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Single Sign-On 구성](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="956c5-181">다른 웹 브라우저 창에서 GitHub 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="956c5-182">너무 이동**설정** 클릭 **보안**</span><span class="sxs-lookup"><span data-stu-id="956c5-182">Navigate too**Settings** and click **Security**</span></span>

    ![설정](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="956c5-184">Hello 확인 **SAML 인증 사용** 상자 hello Single Sign on 구성 필드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-184">Check hello **Enable SAML authentication** box, revealing hello Single Sign-on configuration fields.</span></span> <span data-ttu-id="956c5-185">그런 다음 Azure AD 구성에 hello single sign on URL 값 tooupdate hello Single sign on URL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-185">Then, use hello single sign-on URL value tooupdate hello Single sign-on URL on Azure AD configuration.</span></span>

    ![설정](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="956c5-187">Hello 다음 필드를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-187">Configure hello following fields:</span></span>

    <span data-ttu-id="956c5-188">a.</span><span class="sxs-lookup"><span data-stu-id="956c5-188">a.</span></span> <span data-ttu-id="956c5-189">**로그온 URL**: 입력 **SAML에서 Single sign-on 서비스 URL** hello에서 **GitHub 구성** Azure ad 섹션</span><span class="sxs-lookup"><span data-stu-id="956c5-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="956c5-190">b.</span><span class="sxs-lookup"><span data-stu-id="956c5-190">b.</span></span> <span data-ttu-id="956c5-191">**발급자**: 입력 **SAML 엔터티 ID** hello에서 **GitHub 구성** Azure ad 섹션</span><span class="sxs-lookup"><span data-stu-id="956c5-191">**Issuer**: Enter **SAML Entity ID** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="956c5-192">c.</span><span class="sxs-lookup"><span data-stu-id="956c5-192">c.</span></span> <span data-ttu-id="956c5-193">**공용 인증서**: hello Open "인증서 시작" 및 "최종 인증서"를 포함 하 여 메모장 및 복사 hello 내용에서 Azure AD에서 인증서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-193">**Public Certificate**: Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![설정](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="956c5-195">클릭 **테스트 SAML 구성** tooconfirm 하는 SSO 도중 발생 한 오류 없음이나 유효성 검사에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-195">Click on **Test SAML configuration** tooconfirm that no validation failures or errors during SSO.</span></span>

    ![설정](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="956c5-197">페이지 맨 아래에 있는 **저장**</span><span class="sxs-lookup"><span data-stu-id="956c5-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="956c5-198">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="956c5-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="956c5-199">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-199">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="956c5-201">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="956c5-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="956c5-202">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-202">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="956c5-204">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-204">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="956c5-206">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="956c5-206">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="956c5-208">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="956c5-210">a.</span><span class="sxs-lookup"><span data-stu-id="956c5-210">a.</span></span> <span data-ttu-id="956c5-211">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="956c5-212">b.</span><span class="sxs-lookup"><span data-stu-id="956c5-212">b.</span></span> <span data-ttu-id="956c5-213">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="956c5-214">c.</span><span class="sxs-lookup"><span data-stu-id="956c5-214">c.</span></span> <span data-ttu-id="956c5-215">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="956c5-216">d.</span><span class="sxs-lookup"><span data-stu-id="956c5-216">d.</span></span> <span data-ttu-id="956c5-217">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="956c5-218">GitHub 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="956c5-218">Creating a GitHub test user</span></span>

<span data-ttu-id="956c5-219">tooenable Azure AD 사용자가 toolog GitHub에 주문 하 고, GitHub에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-219">In order tooenable Azure AD users toolog into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="956c5-220">GitHub의 hello 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-220">In hello case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="956c5-221">**사용자 계정 수행 tooprovision hello 다음 단계:**</span><span class="sxs-lookup"><span data-stu-id="956c5-221">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="956c5-222">관리자 권한으로 GitHub 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-222">Log in tooyour GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="956c5-223">**피플**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-223">Click **People**.</span></span>

    <span data-ttu-id="956c5-224">![사람](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "사람")</span><span class="sxs-lookup"><span data-stu-id="956c5-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="956c5-225">**멤버 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-225">Click **Invite member**.</span></span>

    <span data-ttu-id="956c5-226">![사용자 초대](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "사용자 초대")</span><span class="sxs-lookup"><span data-stu-id="956c5-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="956c5-227">Hello에 **초대 멤버** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-227">On hello **Invite member** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="956c5-228">a.</span><span class="sxs-lookup"><span data-stu-id="956c5-228">a.</span></span> <span data-ttu-id="956c5-229">Hello에 **전자 메일** textbox Britta Simon 계정의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="956c5-230">![피플 초대](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "피플 초대")</span><span class="sxs-lookup"><span data-stu-id="956c5-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="956c5-231">b.</span><span class="sxs-lookup"><span data-stu-id="956c5-231">b.</span></span> <span data-ttu-id="956c5-232">**초대 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="956c5-233">![피플 초대](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "피플 초대")</span><span class="sxs-lookup"><span data-stu-id="956c5-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="956c5-234">hello Azure Active Directory 계정 소유자 전자 메일을 받게 되 고 링크 tooconfirm 자신의 계정을 활성화 되기 전에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-234">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="956c5-235">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="956c5-236">이 섹션에서는 액세스 tooGitHub 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooGitHub.</span></span>

![사용자 할당][200] 

<span data-ttu-id="956c5-238">**tooassign Britta Simon tooGitHub hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="956c5-238">**tooassign Britta Simon tooGitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="956c5-239">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-239">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="956c5-241">Hello 응용 프로그램 목록에서 선택 **GitHub.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-241">In hello applications list, select **GitHub.com**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="956c5-243">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="956c5-245">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-245">Click **Add** button.</span></span> <span data-ttu-id="956c5-246">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="956c5-248">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="956c5-249">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="956c5-250">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="956c5-251">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="956c5-251">Testing single sign-on</span></span>

<span data-ttu-id="956c5-252">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-252">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="956c5-253">Hello 액세스 패널에서에서 hello GitHub 타일을 클릭할 때 로그온 tooyour GitHub 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-253">When you click hello GitHub tile in hello Access Panel, you should get signed-on tooyour GitHub application.</span></span> <span data-ttu-id="956c5-254">개인 계정으로는 조직 계정을 하지만, 그때 필요 toolog로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="956c5-254">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="956c5-255">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="956c5-255">Additional resources</span></span>

* [<span data-ttu-id="956c5-256">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="956c5-256">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="956c5-257">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="956c5-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png

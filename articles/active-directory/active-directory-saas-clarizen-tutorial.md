---
title: "자습서: Clarizen과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Clarizen 사이입니다."
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
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="24316-103">자습서: Clarizen과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="24316-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="24316-104">이 자습서에 설명 어떻게 toointegrate Clarizen로 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24316-104">In this tutorial, you learn how toointegrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="24316-105">이 통합에서는 다음과 같은 이점을 hello:</span><span class="sxs-lookup"><span data-stu-id="24316-105">This integration gives you hello following benefits:</span></span>

- <span data-ttu-id="24316-106">제어할 수 있습니다, 액세스 tooClarizen을 지닌 Azure AD에서.</span><span class="sxs-lookup"><span data-stu-id="24316-106">You can control, in Azure AD, who has access tooClarizen.</span></span>
- <span data-ttu-id="24316-107">자동으로 로그인 한 tooClarizen (single sign on)는 Azure AD 계정 사용 하 여 사용자가 toobe를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24316-107">You can enable your users toobe automatically signed in tooClarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="24316-108">하나의 중앙 위치에 hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24316-108">You can manage your accounts in one central location, hello Azure portal.</span></span>

<span data-ttu-id="24316-109">이 자습서의 hello 시나리오의 두 가지 주요 작업으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24316-109">hello scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="24316-110">Hello 갤러리에서 Clarizen을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-110">Add Clarizen from hello gallery.</span></span>
2. <span data-ttu-id="24316-111">Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="24316-112">Azure AD와의 SaaS(Software as a Service) 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24316-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24316-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="24316-113">Prerequisites</span></span>
<span data-ttu-id="24316-114">Clarizen와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-114">tooconfigure Azure AD integration with Clarizen, you need hello following items:</span></span>

- <span data-ttu-id="24316-115">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="24316-115">An Azure AD subscription</span></span>
- <span data-ttu-id="24316-116">Single Sign-On이 활성화된 Clarizen 구독</span><span class="sxs-lookup"><span data-stu-id="24316-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="24316-117">이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="24316-117">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="24316-118">테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24316-119">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="24316-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="24316-120">Azure AD 테스트 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24316-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-hello-gallery"></a><span data-ttu-id="24316-121">Clarizen hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="24316-121">Add Clarizen from hello gallery</span></span>
<span data-ttu-id="24316-122">Clarizen의 tooconfigure hello 통합 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Clarizen을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-122">tooconfigure hello integration of Clarizen into Azure AD, add Clarizen from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="24316-123">Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 창에서 클릭 hello **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-123">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 아이콘][1]

2. <span data-ttu-id="24316-125">**엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="24316-126">그런 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-126">Then click **All applications**.</span></span>

    ![“엔터프라이즈 응용 프로그램” 및 “모든 응용 프로그램” 클릭][2]

3. <span data-ttu-id="24316-128">Hello 클릭 **추가** hello hello 대화 상자 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-128">Click hello **Add** button at hello top of hello dialog box.</span></span>

    ![hello "추가" 단추][3]

4. <span data-ttu-id="24316-130">Hello 검색 상자에 입력 **Clarizen**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-130">In hello search box, type **Clarizen**.</span></span>

    !["Clarizen" hello 검색 상자에 입력](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="24316-132">Hello 결과 창에서 선택 **Clarizen**, 클릭 하 고 **추가** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-132">In hello results pane, select **Clarizen**, and then click **Add** tooadd hello application.</span></span>

    ![Clarizen hello 결과 창에서 선택](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="24316-134">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="24316-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="24316-135">다음 섹션 hello, 구성 하 고와 Clarizen Britta Simon hello 테스트 사용자에 따라 Azure AD에서 single sign-on 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-135">In hello following sections, you configure and test Azure AD single sign-on with Clarizen based on hello test user Britta Simon.</span></span>

<span data-ttu-id="24316-136">Single sign on toowork에 대 한 Azure AD는 tooknow Clarizen에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-136">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clarizen is tooa user in Azure AD.</span></span> <span data-ttu-id="24316-137">즉, Azure AD 사용자와 Clarizen에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-137">In other words, a link relationship between an Azure AD user and hello related user in Clarizen needs toobe established.</span></span> <span data-ttu-id="24316-138">Hello 값을 할당 하 여이 링크 관계를 설정할 **사용자 이름** 의 hello 값으로 Azure AD에서 **Username** Clarizen에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24316-138">You establish this link relationship by assigning hello value of **user name** in Azure AD as hello value of **Username** in Clarizen.</span></span>

<span data-ttu-id="24316-139">tooconfigure와 Clarizen 빌딩 블록을 다음 전체 hello 사용 하 여 Azure AD에서 single sign-on 테스트:</span><span class="sxs-lookup"><span data-stu-id="24316-139">tooconfigure and test Azure AD single sign-on with Clarizen, complete hello following building blocks:</span></span>

1. <span data-ttu-id="24316-140">**[Azure AD single sign-on 구성](#configure-azure-ad-single-sign-on) ** tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24316-141">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user) ** Britta Simon와 Azure AD에서 single sign-on tootest 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24316-142">**[Clarizen 테스트 사용자 만들기](#create-a-clarizen-test-user) ** toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Clarizen에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** toohave a counterpart of Britta Simon in Clarizen that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="24316-143">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user) ** tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24316-144">**[Single sign on 테스트](#test-single-sign-on) ** tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="24316-144">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="24316-145">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="24316-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="24316-146">Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 하 고 Clarizen 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-146">Enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="24316-147">Hello hello에 Azure 포털에서에서 **Clarizen** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-147">In hello Azure portal, on hello **Clarizen** application integration page, click **Single sign-on**.</span></span>

    !["Single sign-on" 클릭][4]

2. <span data-ttu-id="24316-149">Hello에 **Single sign on** 대화 상자에 대 한 **모드**선택, **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-149">In hello **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** tooenable single sign-on.</span></span>

    !["SAML 기반 로그온" 선택](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="24316-151">Hello에 **Clarizen 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-151">In hello **Clarizen Domain and URLs** section, perform hello following steps:</span></span>

    ![식별자 및 회신 URL 상자](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="24316-153">a.</span><span class="sxs-lookup"><span data-stu-id="24316-153">a.</span></span> <span data-ttu-id="24316-154">Hello에 **식별자** 으로 유형 hello 값 상자의: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="24316-154">In hello **Identifier** box, type hello value as: **Clarizen**</span></span>

    <span data-ttu-id="24316-155">b.</span><span class="sxs-lookup"><span data-stu-id="24316-155">b.</span></span> <span data-ttu-id="24316-156">Hello에 **회신 URL** hello 패턴을 사용 하 여 URL을 입력 합니다: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="24316-156">In hello **Reply URL** box, type a URL by using hello following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="24316-157">이들은 hello 실제 값입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-157">These are not hello real values.</span></span> <span data-ttu-id="24316-158">Toouse hello 실제 id를 포함 하 고 회신 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-158">You have toouse hello actual identifier and reply URL.</span></span> <span data-ttu-id="24316-159">여기 hello 식별자 대로 문자열 hello 고유 값을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="24316-159">Here we suggest that you use hello unique value of a string as hello identifier.</span></span> <span data-ttu-id="24316-160">tooget hello 실제 값, 연락처 hello [Clarizen 지원 팀](https://success.clarizen.com/hc/en-us/requests/new)합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-160">tooget hello actual values, contact hello [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="24316-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **새 인증서 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-161">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    !["새 인증서 만들기" 클릭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="24316-163">Hello에 **새 인증서 만들기** 대화 상자, hello 달력 아이콘을 클릭 하 고 만료 날짜를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-163">In hello **Create New Certificate** dialog box, click hello calendar icon and select an expiry date.</span></span> <span data-ttu-id="24316-164">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-164">Then click **Save**.</span></span>

    ![만료 날짜 선택 및 저장](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="24316-166">Hello에 **SAML 서명 인증서** 섹션에서 **새 인증서를 활성화할**, 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-166">In hello **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Hello 활성화 될 때 새 인증서 hello에 대 한 확인란을 선택 하면](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="24316-168">Hello에 **롤오버 인증서** 대화 상자를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-168">In hello **Rollover certificate** dialog box, click **OK**.</span></span>

    ![원하는 toomake hello 인증서 활성 tooconfirm "확인"을 클릭 하면](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="24316-170">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-170">In hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    !["(Base64) 인증서" toostart hello 다운로드를 클릭 하면](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="24316-172">Hello에 **Clarizen 구성** 섹션에서 클릭 **구성 Clarizen** tooopen hello **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="24316-172">In hello **Clarizen Configuration** section, click **Configure Clarizen** tooopen hello **Configure sign-on** window.</span></span>

    !["Clarizen 구성" 클릭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![파일 및 URL을 포함하는 "로그온 구성" 창](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="24316-175">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Clarizen 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-175">In a different web browser window, sign in tooyour Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="24316-176">사용자 이름을 클릭한 다음 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="24316-177">![사용자 이름 아래에서 "설정" 클릭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "설정")</span><span class="sxs-lookup"><span data-stu-id="24316-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="24316-178">Hello 클릭 **전역 설정** 탭 합니다. 그런 다음 다음 너무**페더레이션 인증**, 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-178">Click hello **Global Settings** tab. Then, next too**Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="24316-179">![“전역 설정” 탭](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "전역 설정")</span><span class="sxs-lookup"><span data-stu-id="24316-179">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="24316-180">Hello에 **페더레이션 인증** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-180">In hello **Federated Authentication** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="24316-181">![“페더레이션 인증” 대화 상자](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "페더레이션 인증")</span><span class="sxs-lookup"><span data-stu-id="24316-181">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="24316-182">a.</span><span class="sxs-lookup"><span data-stu-id="24316-182">a.</span></span> <span data-ttu-id="24316-183">**페더레이션 인증 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="24316-184">b.</span><span class="sxs-lookup"><span data-stu-id="24316-184">b.</span></span> <span data-ttu-id="24316-185">클릭 **업로드** tooupload 다운로드 한 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-185">Click **Upload** tooupload your downloaded certificate.</span></span>

    <span data-ttu-id="24316-186">c.</span><span class="sxs-lookup"><span data-stu-id="24316-186">c.</span></span> <span data-ttu-id="24316-187">Hello에 **로그인 URL** 의 hello 값 입력 **SAML Single Sign-on 서비스 URL** hello Azure AD 응용 프로그램 구성 창에서.</span><span class="sxs-lookup"><span data-stu-id="24316-187">In hello **Sign-in URL** box, enter hello value of **SAML Single Sign-On Service URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="24316-188">d.</span><span class="sxs-lookup"><span data-stu-id="24316-188">d.</span></span> <span data-ttu-id="24316-189">Hello에 **Sign-out URL** 의 hello 값 입력 **Sign-Out URL** hello Azure AD 응용 프로그램 구성 창에서.</span><span class="sxs-lookup"><span data-stu-id="24316-189">In hello **Sign-out URL** box, enter hello value of **Sign-Out URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="24316-190">e.</span><span class="sxs-lookup"><span data-stu-id="24316-190">e.</span></span> <span data-ttu-id="24316-191">**POST 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-191">Select **Use POST**.</span></span>

    <span data-ttu-id="24316-192">f.</span><span class="sxs-lookup"><span data-stu-id="24316-192">f.</span></span> <span data-ttu-id="24316-193">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="24316-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="24316-194">Create an Azure AD test user</span></span>
<span data-ttu-id="24316-195">Azure 포털 hello Britta Simon 이라는 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24316-195">In hello Azure portal, create a test user called Britta Simon.</span></span>

![Azure AD hello 테스트 사용자의 이름 및 전자 메일 주소][100]

1. <span data-ttu-id="24316-197">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-197">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 아이콘](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="24316-199">클릭 **사용자 및 그룹**, 클릭 하 고 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-199">Click **Users and groups**, and then click **All users** toodisplay hello list of users.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 클릭](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="24316-201">Hello 대화 상자의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="24316-201">At hello top of hello dialog box, click **Add** tooopen hello **User** dialog box.</span></span>

    ![hello "추가" 단추](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="24316-203">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-203">In hello **User** dialog box, perform hello following steps:</span></span>

    ![이름, 전자 메일 주소 및 암호가 입력된 "사용자" 대화 상자](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="24316-205">a.</span><span class="sxs-lookup"><span data-stu-id="24316-205">a.</span></span> <span data-ttu-id="24316-206">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-206">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24316-207">b.</span><span class="sxs-lookup"><span data-stu-id="24316-207">b.</span></span> <span data-ttu-id="24316-208">Hello에 **사용자 이름** 상자의의 hello Britta Simon 계정 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-208">In hello **User name** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="24316-209">c.</span><span class="sxs-lookup"><span data-stu-id="24316-209">c.</span></span> <span data-ttu-id="24316-210">선택 **암호 표시** hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-210">Select **Show Password** and write down hello value of **Password**.</span></span>

    <span data-ttu-id="24316-211">d.</span><span class="sxs-lookup"><span data-stu-id="24316-211">d.</span></span> <span data-ttu-id="24316-212">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="24316-213">Clarizen 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="24316-213">Create a Clarizen test user</span></span>
<span data-ttu-id="24316-214">tooClarizen에 Azure AD 사용자가 toosign tooenable, 사용자 계정을 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-214">tooenable Azure AD users toosign in tooClarizen, you must provision user accounts.</span></span> <span data-ttu-id="24316-215">Hello Clarizen의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-215">In hello case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="24316-216">관리자 권한으로 Clarizen 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-216">Sign in tooyour Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="24316-217">**피플**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-217">Click **People**.</span></span>

    <span data-ttu-id="24316-218">!["피플" 클릭](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "피플")</span><span class="sxs-lookup"><span data-stu-id="24316-218">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="24316-219">**사용자 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-219">Click **Invite User**.</span></span>

    <span data-ttu-id="24316-220">!["사용자 초대" 단추](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "사용자 초대")</span><span class="sxs-lookup"><span data-stu-id="24316-220">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="24316-221">Hello에 **사용자 초대** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-221">In hello **Invite People** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="24316-222">!["피플 초대" 대화 상자](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "피플 초대")</span><span class="sxs-lookup"><span data-stu-id="24316-222">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="24316-223">a.</span><span class="sxs-lookup"><span data-stu-id="24316-223">a.</span></span> <span data-ttu-id="24316-224">Hello에 **전자 메일** 상자의의 hello Britta Simon 계정 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-224">In hello **Email** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="24316-225">b.</span><span class="sxs-lookup"><span data-stu-id="24316-225">b.</span></span> <span data-ttu-id="24316-226">**초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="24316-227">hello Azure Active Directory 계정 소유자 전자 메일을 받게 되 고 링크 tooconfirm 자신의 계정을 활성화 되기 전에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24316-227">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="24316-228">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-228">Assign hello Azure AD test user</span></span>
<span data-ttu-id="24316-229">그녀의 액세스 tooClarizen 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-229">Enable Britta Simon toouse Azure single sign-on by granting her access tooClarizen.</span></span>

![할당된 테스트 사용자][200]

1. <span data-ttu-id="24316-231">Azure 포털 hello hello 응용 프로그램 보기를 열고, toohello 디렉터리 보기 찾아보기를 클릭 **엔터프라이즈 응용 프로그램**, 클릭 하 고 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-231">In hello Azure portal, open hello applications view, browse toohello directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![“엔터프라이즈 응용 프로그램” 및 “모든 응용 프로그램” 클릭][201]

2. <span data-ttu-id="24316-233">Hello 응용 프로그램 목록에서 선택 **Clarizen**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-233">In hello applications list, select **Clarizen**.</span></span>

    ![Clarizen hello 목록에 선택](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="24316-235">Hello 왼쪽된 창에서 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-235">In hello left pane, click **Users and groups**.</span></span>

    ![“사용자 및 그룹” 클릭][202]

4. <span data-ttu-id="24316-237">Hello 클릭 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-237">Click hello **Add** button.</span></span> <span data-ttu-id="24316-238">그런 다음, hello **할당 추가** 대화 상자에서 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-238">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![hello "추가" 단추 및 hello "할당 추가" 대화 상자][203]

5. <span data-ttu-id="24316-240">Hello에 **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24316-240">In hello **Users and groups** dialog box, select **Britta Simon** in hello list of users.</span></span>

6. <span data-ttu-id="24316-241">Hello에 **사용자 및 그룹** 대화 상자를 클릭 hello **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-241">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="24316-242">Hello에 **할당 추가** 대화 상자를 클릭 hello **할당** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-242">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="24316-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="24316-243">Test single sign-on</span></span>
<span data-ttu-id="24316-244">Hello 액세스 패널을 사용 하 여 Azure AD single sign on 구성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="24316-244">Test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="24316-245">Hello 액세스 패널에서에서 hello Clarizen 타일을 클릭 하면 해야 자동으로 로그인 될 tooyour Clarizen 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="24316-245">When you click hello Clarizen tile in hello Access Panel, you should be automatically signed in tooyour Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24316-246">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="24316-246">Additional resources</span></span>

* [<span data-ttu-id="24316-247">방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="24316-247">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24316-248">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="24316-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png

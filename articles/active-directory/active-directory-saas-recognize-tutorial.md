---
title: "자습서: Recognize와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 인식 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="85a1b-103">자습서: Recognize와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="85a1b-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="85a1b-104">이 자습서에 설명 toointegrate Azure Active Directory (Azure AD)와 어떻게 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-104">In this tutorial, you learn how toointegrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85a1b-105">다음 이점을 hello로 제공 인식 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="85a1b-105">Integrating Recognize with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="85a1b-106">액세스 tooRecognize을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-106">You can control in Azure AD who has access tooRecognize</span></span>
- <span data-ttu-id="85a1b-107">프로그램 사용자 tooautomatically get 로그온 tooRecognize (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-107">You can enable your users tooautomatically get signed-on tooRecognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="85a1b-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="85a1b-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85a1b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="85a1b-110">Prerequisites</span></span>

<span data-ttu-id="85a1b-111">tooconfigure Azure AD 통합 다음 항목 hello 해야 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-111">tooconfigure Azure AD integration with Recognize, you need hello following items:</span></span>

- <span data-ttu-id="85a1b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="85a1b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85a1b-113">Recognize Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="85a1b-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85a1b-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85a1b-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85a1b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="85a1b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85a1b-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85a1b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="85a1b-118">Scenario description</span></span>
<span data-ttu-id="85a1b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85a1b-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85a1b-121">인식은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="85a1b-121">Adding Recognize from hello gallery</span></span>
2. <span data-ttu-id="85a1b-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="85a1b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-hello-gallery"></a><span data-ttu-id="85a1b-123">인식은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="85a1b-123">Adding Recognize from hello gallery</span></span>
<span data-ttu-id="85a1b-124">tooconfigure hello와의 통합 인식 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd 인식 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-124">tooconfigure hello integration of Recognize into Azure AD, you need tooadd Recognize from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="85a1b-125">**hello 갤러리에서 인식 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="85a1b-125">**tooadd Recognize from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a1b-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="85a1b-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="85a1b-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="85a1b-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="85a1b-133">Hello 검색 상자에 입력 **인식**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-133">In hello search box, type **Recognize**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="85a1b-135">Hello 결과 패널에서 선택 **인식**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-135">In hello results panel, select **Recognize**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="85a1b-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="85a1b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="85a1b-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Recognize에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="85a1b-139">Single sign on toowork에 대 한 Azure AD는 tooknow 인식에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Recognize is tooa user in Azure AD.</span></span> <span data-ttu-id="85a1b-140">즉, Azure AD 사용자 및 인식에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-140">In other words, a link relationship between an Azure AD user and hello related user in Recognize needs toobe established.</span></span>

<span data-ttu-id="85a1b-141">인식, hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-141">In Recognize, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="85a1b-142">tooconfigure 및 테스트 Azure AD single sign on 구성 요소를 다음 toocomplete hello 해야 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-142">tooconfigure and test Azure AD single sign-on with Recognize, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="85a1b-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="85a1b-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85a1b-145">**[인식 테스트 사용자 만들기](#creating-a-recognize-test-user)**  -toohave Britta Simon 인식 하는 사용자의 연결 된 Azure AD toohello 표현에에서 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - toohave a counterpart of Britta Simon in Recognize that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="85a1b-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85a1b-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="85a1b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="85a1b-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="85a1b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="85a1b-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 인식 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="85a1b-150">**Azure AD tooconfigure single sign on, 인식 된 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="85a1b-150">**tooconfigure Azure AD single sign-on with Recognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a1b-151">Hello hello에 Azure 포털에서에서 **인식** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-151">In hello Azure portal, on hello **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="85a1b-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="85a1b-155">Hello에 **인식 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-155">On hello **Recognize Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="85a1b-157">a.</span><span class="sxs-lookup"><span data-stu-id="85a1b-157">a.</span></span> <span data-ttu-id="85a1b-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="85a1b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="85a1b-159">b.</span><span class="sxs-lookup"><span data-stu-id="85a1b-159">b.</span></span> <span data-ttu-id="85a1b-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="85a1b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="85a1b-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-161">These values are not real.</span></span> <span data-ttu-id="85a1b-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="85a1b-163">연락처 [인식 클라이언트 지원 팀](mailto:support@recognizeapp.com) hello hello 자습서의 뒷부분에서 설명 하는 SSO 설정 섹션에서에서 hello 서비스 공급자 메타 데이터 URL을 열어 식별자 값을 얻을 수을를 가져오고 로그온 URL 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening hello Service Provider Metadata URL from hello SSO Settings section that is explained later in hello tutorial.</span></span> <span data-ttu-id="85a1b-164">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-164">.</span></span> 
 
4. <span data-ttu-id="85a1b-165">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="85a1b-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-167">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="85a1b-169">Hello에 **구성 인식** 섹션에서 클릭 **구성 인식** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="85a1b-169">On hello **Recognize Configuration** section, click **Configure Recognize** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="85a1b-170">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="85a1b-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="85a1b-172">다른 웹 브라우저 창에서 관리자 권한으로 로그온 tooyour 인식 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-172">In a different web browser window, sign-on tooyour Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="85a1b-173">Hello 오른쪽 위 모서리를 클릭 **메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-173">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="85a1b-174">너무 이동**회사 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-174">Go too**Company Admin**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="85a1b-176">Hello 왼쪽된 탐색 창에서 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-176">On hello left navigation pane, click **Settings**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="85a1b-178">Hello 다음 단계를 수행 **SSO 설정** 섹션.</span><span class="sxs-lookup"><span data-stu-id="85a1b-178">Perform hello following steps on **SSO Settings** section.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="85a1b-180">a.</span><span class="sxs-lookup"><span data-stu-id="85a1b-180">a.</span></span> <span data-ttu-id="85a1b-181">**SSO 사용**에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="85a1b-182">b.</span><span class="sxs-lookup"><span data-stu-id="85a1b-182">b.</span></span> <span data-ttu-id="85a1b-183">Hello에 **IDP 엔터티 ID** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="85a1b-184">c.</span><span class="sxs-lookup"><span data-stu-id="85a1b-184">c.</span></span> <span data-ttu-id="85a1b-185">Hello에 **Sso 대상 url** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-185">In hello **Sso target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="85a1b-186">d.</span><span class="sxs-lookup"><span data-stu-id="85a1b-186">d.</span></span> <span data-ttu-id="85a1b-187">Hello에 **Slo 대상 url** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-187">In hello **Slo target url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="85a1b-188">e.</span><span class="sxs-lookup"><span data-stu-id="85a1b-188">e.</span></span> <span data-ttu-id="85a1b-189">프로그램 다운로드 한 열고 **인증서 (Base64)** 내용을 클립보드의 콘텐츠 복사 hello 메모장에서 파일을 붙여넣을 toohello **인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-189">Open your downloaded **Certificate (Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="85a1b-190">f.</span><span class="sxs-lookup"><span data-stu-id="85a1b-190">f.</span></span> <span data-ttu-id="85a1b-191">Hello 클릭 **설정을 저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-191">Click hello **Save settings** button.</span></span> 

11. <span data-ttu-id="85a1b-192">Hello 옆에 있는 **SSO 설정** 섹션에서 아래 hello URL 복사 **서비스 공급자 메타 데이터 url**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-192">Beside hello **SSO Settings** section, copy hello URL under **Service Provider Metadata url**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="85a1b-194">열기 hello **메타 데이터 URL 링크** 빈 브라우저 toodownload hello 메타 데이터 문서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-194">Open hello **Metadata URL link** under a blank browser toodownload hello metadata document.</span></span> <span data-ttu-id="85a1b-195">다음 hello EntityDescriptor value(entityID) hello 파일에서 복사 하 고에 붙여 **식별자** 텍스트 상자로 **인식 도메인 및 Url 섹션** Azure 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-195">Then copy hello EntityDescriptor value(entityID) from hello file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="85a1b-197">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="85a1b-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="85a1b-198">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="85a1b-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="85a1b-199">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="85a1b-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="85a1b-200">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="85a1b-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="85a1b-201">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="85a1b-203">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="85a1b-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a1b-204">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="85a1b-206">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="85a1b-208">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="85a1b-210">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="85a1b-212">a.</span><span class="sxs-lookup"><span data-stu-id="85a1b-212">a.</span></span> <span data-ttu-id="85a1b-213">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85a1b-214">b.</span><span class="sxs-lookup"><span data-stu-id="85a1b-214">b.</span></span> <span data-ttu-id="85a1b-215">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="85a1b-216">c.</span><span class="sxs-lookup"><span data-stu-id="85a1b-216">c.</span></span> <span data-ttu-id="85a1b-217">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="85a1b-218">d.</span><span class="sxs-lookup"><span data-stu-id="85a1b-218">d.</span></span> <span data-ttu-id="85a1b-219">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="85a1b-220">Recognize 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="85a1b-220">Creating a Recognize test user</span></span>

<span data-ttu-id="85a1b-221">Tooenable Azure AD 사용자가 toolog 인식에 주문 하 고에 인식에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-221">In order tooenable Azure AD users toolog into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="85a1b-222">Hello 인식의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-222">In hello case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="85a1b-223">이 앱은 SCIM 프로비전을 지원하지 않지만 사용자를 프로비전하는 대체 사용자 동기화 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="85a1b-224">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="85a1b-224">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a1b-225">Recognize 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="85a1b-226">Hello 오른쪽 위 모서리를 클릭 **메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-226">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="85a1b-227">너무 이동**회사 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-227">Go too**Company Admin**.</span></span>

3. <span data-ttu-id="85a1b-228">Hello 왼쪽된 탐색 창에서 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-228">On hello left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="85a1b-229">Hello 다음 단계를 수행 **사용자 동기화** 섹션.</span><span class="sxs-lookup"><span data-stu-id="85a1b-229">Perform hello following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="85a1b-230">![새 사용자](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="85a1b-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="85a1b-231">a.</span><span class="sxs-lookup"><span data-stu-id="85a1b-231">a.</span></span> <span data-ttu-id="85a1b-232">**동기화 사용**에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="85a1b-233">b.</span><span class="sxs-lookup"><span data-stu-id="85a1b-233">b.</span></span> <span data-ttu-id="85a1b-234">**동기화 공급자 선택**에서 **Microsoft/Office 365**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="85a1b-235">c.</span><span class="sxs-lookup"><span data-stu-id="85a1b-235">c.</span></span> <span data-ttu-id="85a1b-236">**사용자 동기화 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-236">Click **Run User Sync**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="85a1b-237">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="85a1b-238">이 섹션에서는 tooRecognize 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRecognize.</span></span>

![사용자 할당][200] 

<span data-ttu-id="85a1b-240">**tooassign Britta Simon tooRecognize hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="85a1b-240">**tooassign Britta Simon tooRecognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a1b-241">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="85a1b-243">Hello 응용 프로그램 목록에서 선택 **인식**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-243">In hello applications list, select **Recognize**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="85a1b-245">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="85a1b-247">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-247">Click **Add** button.</span></span> <span data-ttu-id="85a1b-248">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="85a1b-250">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="85a1b-251">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85a1b-252">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="85a1b-253">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="85a1b-253">Testing single sign-on</span></span>

<span data-ttu-id="85a1b-254">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="85a1b-255">Hello 액세스 패널에서에서 hello 인식 타일을 클릭할 때 자동으로 로그온 tooyour 인식 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-255">When you click hello Recognize tile in hello Access Panel, you should get automatically signed-on tooyour Recognize application.</span></span> <span data-ttu-id="85a1b-256">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="85a1b-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="85a1b-257">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="85a1b-257">Additional resources</span></span>

* [<span data-ttu-id="85a1b-258">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="85a1b-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85a1b-259">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="85a1b-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png


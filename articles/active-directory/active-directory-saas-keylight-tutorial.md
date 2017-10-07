---
title: "자습서: LockPath Keylight와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 LockPath Keylight 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="f83a1-103">자습서: Azure Active Directory와 LockPath Keylight 통합</span><span class="sxs-lookup"><span data-stu-id="f83a1-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="f83a1-104">이 자습서에 설명 어떻게 toointegrate LockPath Keylight Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f83a1-104">In this tutorial, you learn how toointegrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f83a1-105">다음 이점을 hello로 제공 LockPath Keylight Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="f83a1-105">Integrating LockPath Keylight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f83a1-106">액세스 tooLockPath Keylight 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-106">You can control in Azure AD who has access tooLockPath Keylight</span></span>
- <span data-ttu-id="f83a1-107">프로그램 사용자 tooautomatically get 로그온 tooLockPath Keylight (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-107">You can enable your users tooautomatically get signed-on tooLockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f83a1-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f83a1-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f83a1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f83a1-110">Prerequisites</span></span>

<span data-ttu-id="f83a1-111">다음 항목 hello가 필요 tooconfigure LockPath Keylight와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-111">tooconfigure Azure AD integration with LockPath Keylight, you need hello following items:</span></span>

- <span data-ttu-id="f83a1-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f83a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f83a1-113">LockPath Keylight Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f83a1-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f83a1-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f83a1-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f83a1-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f83a1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f83a1-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f83a1-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f83a1-118">Scenario description</span></span>
<span data-ttu-id="f83a1-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f83a1-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f83a1-121">LockPath Keylight hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="f83a1-121">Adding LockPath Keylight from hello gallery</span></span>
2. <span data-ttu-id="f83a1-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f83a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-hello-gallery"></a><span data-ttu-id="f83a1-123">LockPath Keylight hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="f83a1-123">Adding LockPath Keylight from hello gallery</span></span>
<span data-ttu-id="f83a1-124">tooconfigure hello와의 통합 LockPath Keylight Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 LockPath Keylight tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-124">tooconfigure hello integration of LockPath Keylight into Azure AD, you need tooadd LockPath Keylight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f83a1-125">**tooadd hello 갤러리에서 LockPath Keylight hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f83a1-125">**tooadd LockPath Keylight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83a1-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f83a1-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f83a1-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="f83a1-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="f83a1-133">Hello 검색 상자에 입력 **LockPath Keylight**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-133">In hello search box, type **LockPath Keylight**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="f83a1-135">Hello 결과 패널에서 선택 **LockPath Keylight**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-135">In hello results panel, select **LockPath Keylight**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f83a1-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f83a1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f83a1-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 LockPath Keylight에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f83a1-139">Single sign on toowork에 대 한 Azure AD는 tooknow LockPath Keylight에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LockPath Keylight is tooa user in Azure AD.</span></span> <span data-ttu-id="f83a1-140">즉, Azure AD 사용자 및 LockPath Keylight에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-140">In other words, a link relationship between an Azure AD user and hello related user in LockPath Keylight needs toobe established.</span></span>

<span data-ttu-id="f83a1-141">LockPath Keylight에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-141">In LockPath Keylight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f83a1-142">tooconfigure 및 LockPath Keylight를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-142">tooconfigure and test Azure AD single sign-on with LockPath Keylight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f83a1-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f83a1-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f83a1-145">**[LockPath Keylight 테스트 사용자 만들기](#creating-a-lockpath-keylight-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 LockPath Keylight에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - toohave a counterpart of Britta Simon in LockPath Keylight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f83a1-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f83a1-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="f83a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f83a1-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f83a1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f83a1-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 LockPath Keylight 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="f83a1-150">**tooconfigure Azure AD single sign on LockPath Keylight와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f83a1-150">**tooconfigure Azure AD single sign-on with LockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83a1-151">Hello hello에 Azure 포털에서에서 **LockPath Keylight** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-151">In hello Azure portal, on hello **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="f83a1-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="f83a1-155">Hello에 **LockPath Keylight 도메인 및 Url** 섹션에서 단계를 수행 하는 hello 수행::</span><span class="sxs-lookup"><span data-stu-id="f83a1-155">On hello **LockPath Keylight Domain and URLs** section, perform hello following steps::</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="f83a1-157">a.</span><span class="sxs-lookup"><span data-stu-id="f83a1-157">a.</span></span> <span data-ttu-id="f83a1-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="f83a1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="f83a1-159">b.</span><span class="sxs-lookup"><span data-stu-id="f83a1-159">b.</span></span> <span data-ttu-id="f83a1-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="f83a1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="f83a1-161">c.</span><span class="sxs-lookup"><span data-stu-id="f83a1-161">c.</span></span> <span data-ttu-id="f83a1-162">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="f83a1-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f83a1-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-163">These values are not real.</span></span> <span data-ttu-id="f83a1-164">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f83a1-165">연락처 [LockPath Keylight 클라이언트 지원 팀](https://www.lockpath.com/contact/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="f83a1-166">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Raw)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-166">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="f83a1-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="f83a1-170">Hello에 **LockPath Keylight 구성** 섹션에서 클릭 **LockPath Keylight 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="f83a1-170">On hello **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f83a1-171">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="f83a1-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="f83a1-173">tooenable LockPath Keylight에서 SSO hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-173">tooenable SSO in LockPath Keylight, perform hello following steps:</span></span>
   
    <span data-ttu-id="f83a1-174">a.</span><span class="sxs-lookup"><span data-stu-id="f83a1-174">a.</span></span> <span data-ttu-id="f83a1-175">로그온 tooyour LockPath Keylight 계정 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-175">Sign-on tooyour LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="f83a1-176">b.</span><span class="sxs-lookup"><span data-stu-id="f83a1-176">b.</span></span> <span data-ttu-id="f83a1-177">Hello 메뉴에서 hello 위에 표시를 클릭 **사람**를 선택 하 고 **Keylight 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-177">In hello menu on hello top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="f83a1-179">c.</span><span class="sxs-lookup"><span data-stu-id="f83a1-179">c.</span></span> <span data-ttu-id="f83a1-180">Hello 왼쪽에 hello treeview에서 클릭 **SAML**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-180">In hello treeview on hello left, click **SAML**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="f83a1-182">d.</span><span class="sxs-lookup"><span data-stu-id="f83a1-182">d.</span></span> <span data-ttu-id="f83a1-183">Hello에 **SAML 설정** 대화 상자를 클릭 하 여 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-183">On hello **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="f83a1-185">Hello에 **SAML 설정 편집** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-185">On hello **Edit SAML Settings** dialog page, perform hello following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="f83a1-187">a.</span><span class="sxs-lookup"><span data-stu-id="f83a1-187">a.</span></span> <span data-ttu-id="f83a1-188">설정 **SAML 인증** 너무**활성**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-188">Set **SAML authentication** too**Active**.</span></span>

    <span data-ttu-id="f83a1-189">b.</span><span class="sxs-lookup"><span data-stu-id="f83a1-189">b.</span></span> <span data-ttu-id="f83a1-190">붙여넣기 hello **SAML Single Sign-on 서비스 URL** hello에 hello Azure 포털에서에서 복사한 값으로 **Id 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="f83a1-191">c.</span><span class="sxs-lookup"><span data-stu-id="f83a1-191">c.</span></span> <span data-ttu-id="f83a1-192">붙여넣기 hello **Single Sign-Out 서비스 URL** hello에 hello Azure 포털에서에서 복사한 값으로 **Identity Provider Logout URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-192">Paste hello **Single Sign-Out Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="f83a1-193">d.</span><span class="sxs-lookup"><span data-stu-id="f83a1-193">d.</span></span> <span data-ttu-id="f83a1-194">클릭 **파일 선택** tooselect 프로그램 다운로드 한 LockPath Keylight 인증서를 클릭 하 고 **열려** tooupload hello 인증서.</span><span class="sxs-lookup"><span data-stu-id="f83a1-194">Click **Choose File** tooselect your downloaded LockPath Keylight certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="f83a1-195">e.</span><span class="sxs-lookup"><span data-stu-id="f83a1-195">e.</span></span> <span data-ttu-id="f83a1-196">설정 **SAML 사용자 Id 위치** 너무**hello subject 문의 NameIdentifier 요소**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-196">Set **SAML User Id location** too**NameIdentifier element of hello subject statement**.</span></span>
    
    <span data-ttu-id="f83a1-197">f.</span><span class="sxs-lookup"><span data-stu-id="f83a1-197">f.</span></span> <span data-ttu-id="f83a1-198">Hello 제공 **Keylight 서비스 공급자** hello 패턴을 사용 하 여: **https://&lt;CompanyName&gt;. keylightgrc.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-198">Provide hello **Keylight Service Provider** using hello following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="f83a1-199">g.</span><span class="sxs-lookup"><span data-stu-id="f83a1-199">g.</span></span> <span data-ttu-id="f83a1-200">설정 **자동 프로 비전 사용자** 너무**활성**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-200">Set **Auto-provision users** too**Active**.</span></span>

    <span data-ttu-id="f83a1-201">h.</span><span class="sxs-lookup"><span data-stu-id="f83a1-201">h.</span></span> <span data-ttu-id="f83a1-202">설정 **자동 프로 비전 계정 유형** 너무**전체 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-202">Set **Auto-provision account type** too**Full User**.</span></span>

    <span data-ttu-id="f83a1-203">i.</span><span class="sxs-lookup"><span data-stu-id="f83a1-203">i.</span></span> <span data-ttu-id="f83a1-204">**Auto-provision security role**(자동 프로비전 보안 역할)에 **Standard User with SAML**(SAML을 사용하는 표준 사용자)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="f83a1-205">j.</span><span class="sxs-lookup"><span data-stu-id="f83a1-205">j.</span></span> <span data-ttu-id="f83a1-206">**Auto-provision security config**(자동 프로비전 보안 구성)에 **Standard User Configuration**(표준 사용자 구성)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="f83a1-207">k.</span><span class="sxs-lookup"><span data-stu-id="f83a1-207">k.</span></span> <span data-ttu-id="f83a1-208">Hello에 **전자 메일 특성** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-208">In hello **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="f83a1-209">l.</span><span class="sxs-lookup"><span data-stu-id="f83a1-209">l.</span></span> <span data-ttu-id="f83a1-210">Hello에 **이름 특성** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-210">In hello **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="f83a1-211">m.</span><span class="sxs-lookup"><span data-stu-id="f83a1-211">m.</span></span> <span data-ttu-id="f83a1-212">Hello에 **성 특성** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-212">In hello **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="f83a1-213">n.</span><span class="sxs-lookup"><span data-stu-id="f83a1-213">n.</span></span> <span data-ttu-id="f83a1-214">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f83a1-215">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="f83a1-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f83a1-216">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="f83a1-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f83a1-217">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f83a1-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f83a1-218">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f83a1-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="f83a1-219">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="f83a1-221">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f83a1-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83a1-222">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-222">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f83a1-224">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-224">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f83a1-226">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-226">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f83a1-228">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-228">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f83a1-230">a.</span><span class="sxs-lookup"><span data-stu-id="f83a1-230">a.</span></span> <span data-ttu-id="f83a1-231">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-231">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f83a1-232">b.</span><span class="sxs-lookup"><span data-stu-id="f83a1-232">b.</span></span> <span data-ttu-id="f83a1-233">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-233">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f83a1-234">c.</span><span class="sxs-lookup"><span data-stu-id="f83a1-234">c.</span></span> <span data-ttu-id="f83a1-235">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-235">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f83a1-236">d.</span><span class="sxs-lookup"><span data-stu-id="f83a1-236">d.</span></span> <span data-ttu-id="f83a1-237">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="f83a1-238">LockPath Keylight 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f83a1-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="f83a1-239">이 섹션에서는 LockPath Keylight에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="f83a1-240">LockPath Keylight는 기본적으로 사용하도록 설정된 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="f83a1-241">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-241">There is no action item for you in this section.</span></span> <span data-ttu-id="f83a1-242">새 사용자는 hello 사용자 아직 존재 하지 않으면 LockPath Keylight에 액세스할 때 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-242">A new user is created when accessing LockPath Keylight if hello user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="f83a1-243">Toocontact hello toocreate 사용자를 수동으로 필요한 경우 필요한 [LockPath Keylight 클라이언트 지원 팀](https://www.lockpath.com/contact/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-243">If you need toocreate a user manually, you need toocontact hello [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f83a1-244">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f83a1-245">이 섹션에서는 액세스 tooLockPath Keylight 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLockPath Keylight.</span></span>

![사용자 할당][200] 

<span data-ttu-id="f83a1-247">**tooassign Britta Simon tooLockPath Keylight, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f83a1-247">**tooassign Britta Simon tooLockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f83a1-248">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f83a1-250">Hello 응용 프로그램 목록에서 선택 **LockPath Keylight**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-250">In hello applications list, select **LockPath Keylight**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="f83a1-252">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="f83a1-254">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-254">Click **Add** button.</span></span> <span data-ttu-id="f83a1-255">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="f83a1-257">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f83a1-258">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f83a1-259">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f83a1-260">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f83a1-260">Testing single sign-on</span></span>

<span data-ttu-id="f83a1-261">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f83a1-262">Hello LockPath Keylight hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour LockPath Keylight 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83a1-262">When you click hello LockPath Keylight tile in hello Access Panel, you should get automatically signed-on tooyour LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f83a1-263">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f83a1-263">Additional resources</span></span>

* [<span data-ttu-id="f83a1-264">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="f83a1-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f83a1-265">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f83a1-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png


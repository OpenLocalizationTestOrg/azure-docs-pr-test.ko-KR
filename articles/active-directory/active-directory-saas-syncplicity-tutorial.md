---
title: "자습서: Syncplicity와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Syncplicity 간에 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="57540-103">자습서: Syncplicity와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="57540-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="57540-104">이 자습서에 설명 어떻게 toointegrate Syncplicity와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57540-104">In this tutorial, you learn how toointegrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57540-105">Azure AD와 Syncplicity 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-105">Integrating Syncplicity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="57540-106">액세스 tooSyncplicity을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57540-106">You can control in Azure AD who has access tooSyncplicity</span></span>
- <span data-ttu-id="57540-107">프로그램 사용자 tooautomatically get 로그온 tooSyncplicity (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57540-107">You can enable your users tooautomatically get signed-on tooSyncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57540-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57540-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="57540-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57540-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="57540-110">Prerequisites</span></span>

<span data-ttu-id="57540-111">Syncplicity와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-111">tooconfigure Azure AD integration with Syncplicity, you need hello following items:</span></span>

- <span data-ttu-id="57540-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="57540-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57540-113">Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="57540-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57540-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57540-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57540-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="57540-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57540-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57540-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57540-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="57540-118">Scenario description</span></span>
<span data-ttu-id="57540-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57540-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57540-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57540-121">Syncplicity는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="57540-121">Adding Syncplicity from hello gallery</span></span>
2. <span data-ttu-id="57540-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="57540-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-hello-gallery"></a><span data-ttu-id="57540-123">Syncplicity는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="57540-123">Adding Syncplicity from hello gallery</span></span>
<span data-ttu-id="57540-124">tooconfigure hello와의 통합 Syncplicity Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Syncplicity tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-124">tooconfigure hello integration of Syncplicity into Azure AD, you need tooadd Syncplicity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="57540-125">**hello 갤러리에서 Syncplicity tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="57540-125">**tooadd Syncplicity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="57540-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57540-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="57540-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="57540-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="57540-133">Hello 검색 상자에 입력 **Syncplicity**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-133">In hello search box, type **Syncplicity**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="57540-135">Hello 결과 패널에서 선택 **Syncplicity**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-135">In hello results panel, select **Syncplicity**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57540-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="57540-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57540-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Syncplicity에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="57540-139">Single sign on toowork에 대 한 Azure AD는 tooknow Syncplicity에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Syncplicity is tooa user in Azure AD.</span></span> <span data-ttu-id="57540-140">즉, Azure AD 사용자와 Syncplicity에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-140">In other words, a link relationship between an Azure AD user and hello related user in Syncplicity needs toobe established.</span></span>

<span data-ttu-id="57540-141">Syncplicity에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-141">In Syncplicity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="57540-142">tooconfigure와 Syncplicity와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-142">tooconfigure and test Azure AD single sign-on with Syncplicity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="57540-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="57540-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57540-145">**[Syncplicity 테스트 사용자 만들기](#creating-a-syncplicity-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Syncplicity에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - toohave a counterpart of Britta Simon in Syncplicity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="57540-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57540-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="57540-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57540-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="57540-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57540-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Syncplicity 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="57540-150">**tooconfigure Azure AD single sign on와 Syncplicity를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="57540-150">**tooconfigure Azure AD single sign-on with Syncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="57540-151">Hello hello에 Azure 포털에서에서 **Syncplicity** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-151">In hello Azure portal, on hello **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="57540-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="57540-155">Hello에 **Syncplicity 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-155">On hello **Syncplicity Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="57540-157">a.</span><span class="sxs-lookup"><span data-stu-id="57540-157">a.</span></span> <span data-ttu-id="57540-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="57540-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="57540-159">b.</span><span class="sxs-lookup"><span data-stu-id="57540-159">b.</span></span> <span data-ttu-id="57540-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="57540-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="57540-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="57540-161">These values are not real.</span></span> <span data-ttu-id="57540-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="57540-163">연락처 [Syncplicity 클라이언트 지원 팀](https://www.syncplicity.com/contact-us) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) tooget these values.</span></span> 
 

4. <span data-ttu-id="57540-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="57540-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="57540-168">Hello에 **Syncplicity 구성** 섹션에서 클릭 **Syncplicity 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="57540-168">On hello **Syncplicity Configuration** section, click **Configure Syncplicity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="57540-169">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="57540-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="57540-171">Tooyour 로그인 **Syncplicity** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-171">Sign in tooyour **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="57540-172">Hello 메뉴에서 hello 위에 표시를 클릭 **관리자**선택, **설정**, 클릭 하 고 **사용자 지정 도메인 및 single sign-on**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-172">In hello menu on hello top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="57540-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="57540-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="57540-174">Hello에 **Single Sign-on (SSO)** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-174">On hello **Single Sign-On (SSO)** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="57540-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="57540-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="57540-176">a.</span><span class="sxs-lookup"><span data-stu-id="57540-176">a.</span></span> <span data-ttu-id="57540-177">Hello에 **사용자 지정 도메인** 도메인 형식 hello 이름 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-177">In hello **Custom Domain** textbox, type hello name of your domain.</span></span>
  
    <span data-ttu-id="57540-178">b.</span><span class="sxs-lookup"><span data-stu-id="57540-178">b.</span></span> <span data-ttu-id="57540-179">**사용**을 **Single Sign-On 상태**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="57540-180">c.</span><span class="sxs-lookup"><span data-stu-id="57540-180">c.</span></span> <span data-ttu-id="57540-181">Hello에 **엔터티 Id** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-181">In hello **Entity Id** textbox, Paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="57540-182">d.</span><span class="sxs-lookup"><span data-stu-id="57540-182">d.</span></span> <span data-ttu-id="57540-183">Hello에 **로그인 페이지 URL** 텍스트 붙여넣기 hello **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-183">In hello **Sign-in page URL** textbox, Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="57540-184">e.</span><span class="sxs-lookup"><span data-stu-id="57540-184">e.</span></span> <span data-ttu-id="57540-185">Hello에 **로그 아웃 페이지 URL** 텍스트 붙여넣기 hello **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-185">In hello **Logout page URL** textbox, Paste hello **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="57540-186">f.</span><span class="sxs-lookup"><span data-stu-id="57540-186">f.</span></span> <span data-ttu-id="57540-187">**Id 공급자 인증서**, 클릭 **파일 선택**, 다음 hello Azure 포털에서에서 다운로드 한 hello 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-187">In **Identity Provider Certificate**, click **Choose file**, and then upload hello certificate which you have downloaded from hello Azure portal.</span></span> 

    <span data-ttu-id="57540-188">g.</span><span class="sxs-lookup"><span data-stu-id="57540-188">g.</span></span> <span data-ttu-id="57540-189">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="57540-190">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="57540-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="57540-191">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="57540-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="57540-192">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57540-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57540-193">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="57540-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="57540-194">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="57540-196">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="57540-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="57540-197">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57540-199">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57540-201">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57540-203">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57540-205">a.</span><span class="sxs-lookup"><span data-stu-id="57540-205">a.</span></span> <span data-ttu-id="57540-206">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57540-207">b.</span><span class="sxs-lookup"><span data-stu-id="57540-207">b.</span></span> <span data-ttu-id="57540-208">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57540-209">c.</span><span class="sxs-lookup"><span data-stu-id="57540-209">c.</span></span> <span data-ttu-id="57540-210">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="57540-211">d.</span><span class="sxs-lookup"><span data-stu-id="57540-211">d.</span></span> <span data-ttu-id="57540-212">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="57540-213">Syncplicity 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="57540-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="57540-214">AAD 사용자 toobe 수 toosign에서, 프로 비전 된 tooSyncplicity 응용 프로그램 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-214">For AAD users toobe able toosign in, they must be provisioned tooSyncplicity application.</span></span> <span data-ttu-id="57540-215">이 섹션에서는 Syncplicity에서 toocreate AAD 사용자 계정을 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-215">This section describes how toocreate AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="57540-216">**사용자 계정 tooSyncplicity tooprovision hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="57540-216">**tooprovision a user account tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="57540-217">Tooyour 로그인 **Syncplicity** 테 넌 트 (예: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="57540-217">Log in tooyour **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="57540-218">**관리자**를 클릭하고 **사용자 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="57540-219">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="57540-220">![사용자 관리](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="57540-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="57540-221">형식 hello **전자 메일 addressess** tooprovision 선택 하려는 AAD 계정의 **사용자** 으로 **역할**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-221">Type hello **Email addressess** of an AAD account you want tooprovision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="57540-222">![계정 정보](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "계정 정보")</span><span class="sxs-lookup"><span data-stu-id="57540-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="57540-223">hello AAD 계정 보유자 메일 링크 tooconfirm 포함 가져오고 hello 계정을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-223">hello AAD account holder  gets an email including a link tooconfirm and activate hello account.</span></span> 
    > 

5. <span data-ttu-id="57540-224">회사에서 새 사용자가 구성원이 되고자 하는 그룹을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="57540-225">![그룹 멤버 자격](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "그룹 멤버 자격")</span><span class="sxs-lookup"><span data-stu-id="57540-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="57540-226">나열된 그룹이 없으면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="57540-227">Hello 폴더 tooplace hello 사용자의 컴퓨터에서 Syncplicity의 제어에서 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-227">Select hello folders you would like tooplace under Syncplicity’s control on hello user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="57540-228">![Syncplicity 폴더](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity 폴더")</span><span class="sxs-lookup"><span data-stu-id="57540-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="57540-229">다른 Syncplicity 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Syncplicity에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="57540-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="57540-230">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="57540-231">이 섹션에서는 tooSyncplicity 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSyncplicity.</span></span>

![사용자 할당][200] 

<span data-ttu-id="57540-233">**tooassign Britta Simon tooSyncplicity hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="57540-233">**tooassign Britta Simon tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="57540-234">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="57540-236">Hello 응용 프로그램 목록에서 선택 **Syncplicity**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-236">In hello applications list, select **Syncplicity**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="57540-238">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="57540-240">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-240">Click **Add** button.</span></span> <span data-ttu-id="57540-241">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="57540-243">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57540-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="57540-244">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57540-245">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57540-246">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="57540-246">Testing single sign-on</span></span>

<span data-ttu-id="57540-247">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="57540-248">Hello 액세스 패널에서에서 hello Syncplicity 타일을 클릭할 때 자동으로 로그온 tooyour Syncplicity 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57540-248">When you click hello Syncplicity tile in hello Access Panel, you should get automatically signed-on tooyour Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="57540-249">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="57540-249">Additional resources</span></span>

* [<span data-ttu-id="57540-250">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="57540-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57540-251">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="57540-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png


---
title: "자습서: Brightspace by Desire2Learn와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Brightspace by Desire2Learn 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 99d03dc50defcb291a651a5415e30baab39e1e77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="fed77-103">자습서: Brightspace by Desire2Learn와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="fed77-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>

<span data-ttu-id="fed77-104">이 자습서에 설명 어떻게 toointegrate Brightspace by Desire2Learn Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fed77-104">In this tutorial, you learn how toointegrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fed77-105">Azure AD와 Brightspace by Desire2Learn 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fed77-106">액세스 tooBrightspace by Desire2Learn 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-106">You can control in Azure AD who has access tooBrightspace by Desire2Learn</span></span>
- <span data-ttu-id="fed77-107">에 사용자가 tooautomatically get 로그온 tooBrightspace by Desire2Learn에 사용 하도록 설정할 수 있습니다 (Single Sign-on)는 Azure AD 계정을 사용</span><span class="sxs-lookup"><span data-stu-id="fed77-107">You can enable your users tooautomatically get signed-on tooBrightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fed77-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fed77-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fed77-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fed77-110">Prerequisites</span></span>

<span data-ttu-id="fed77-111">Brightspace by Desire2Learn와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-111">tooconfigure Azure AD integration with Brightspace by Desire2Learn, you need hello following items:</span></span>

- <span data-ttu-id="fed77-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="fed77-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fed77-113">Brightspace Desire2Learn single sign-on이 사용된 구독</span><span class="sxs-lookup"><span data-stu-id="fed77-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fed77-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fed77-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fed77-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="fed77-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fed77-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fed77-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="fed77-118">Scenario description</span></span>
<span data-ttu-id="fed77-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fed77-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fed77-121">Brightspace by Desire2Learn hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="fed77-121">Adding Brightspace by Desire2Learn from hello gallery</span></span>
2. <span data-ttu-id="fed77-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="fed77-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-brightspace-by-desire2learn-from-hello-gallery"></a><span data-ttu-id="fed77-123">Brightspace by Desire2Learn hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="fed77-123">Adding Brightspace by Desire2Learn from hello gallery</span></span>
<span data-ttu-id="fed77-124">tooconfigure hello와의 통합 Brightspace by Desire2Learn Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Brightspace by Desire2Learn tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-124">tooconfigure hello integration of Brightspace by Desire2Learn into Azure AD, you need tooadd Brightspace by Desire2Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fed77-125">**Brightspace by Desire2Learn hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fed77-125">**tooadd Brightspace by Desire2Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fed77-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fed77-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fed77-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="fed77-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="fed77-133">Hello 검색 상자에 입력 **Brightspace by Desire2Learn**합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-133">In hello search box, type **Brightspace by Desire2Learn**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_search.png)

5. <span data-ttu-id="fed77-135">Hello 결과 패널에서 선택 **Brightspace by Desire2Learn**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-135">In hello results panel, select **Brightspace by Desire2Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fed77-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="fed77-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fed77-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Brightspace by Desire2Learn에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fed77-139">Single sign on toowork에 대 한 Azure AD는 tooknow Brightspace by Desire2Learn에에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Brightspace by Desire2Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="fed77-140">즉, Azure AD 사용자와 Brightspace by Desire2Learn에에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-140">In other words, a link relationship between an Azure AD user and hello related user in Brightspace by Desire2Learn needs toobe established.</span></span>

<span data-ttu-id="fed77-141">Brightspace by Desire2Learn에에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-141">In Brightspace by Desire2Learn, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fed77-142">tooconfigure와 Brightspace by Desire2Learn 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-142">tooconfigure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fed77-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fed77-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fed77-145">**[Brightspace by Desire2Learn 테스트 사용자 만들기](#creating-a-brightspace-by-desire2learn-test-user)**  -toohave Britta Simon Brightspace by Desire2Learn 표현인 연결 된 toohello Azure AD의 사용자에에서 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - toohave a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fed77-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fed77-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="fed77-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fed77-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="fed77-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fed77-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Desire2Learn 응용 프로그램에 의해 Brightspace에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span></span>

<span data-ttu-id="fed77-150">**Azure AD tooconfigure single sign on와 Brightspace by Desire2Learn hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fed77-150">**tooconfigure Azure AD single sign-on with Brightspace by Desire2Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="fed77-151">Hello hello에 Azure 포털에서에서 **Brightspace by Desire2Learn** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-151">In hello Azure portal, on hello **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="fed77-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_samlbase.png)

3. <span data-ttu-id="fed77-155">Hello에 **Brightspace by Desire2Learn 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-155">On hello **Brightspace by Desire2Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_url.png)

    <span data-ttu-id="fed77-157">a.</span><span class="sxs-lookup"><span data-stu-id="fed77-157">a.</span></span> <span data-ttu-id="fed77-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="fed77-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.tenants.brightspace.com/samlLogin`|
    | `https://<companyname>.desire2learn.com/shibboleth-sp`|

    <span data-ttu-id="fed77-159">b.</span><span class="sxs-lookup"><span data-stu-id="fed77-159">b.</span></span> <span data-ttu-id="fed77-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span><span class="sxs-lookup"><span data-stu-id="fed77-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fed77-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-161">These values are not real.</span></span> <span data-ttu-id="fed77-162">Hello 실제 식별자 및 회신 URL로이 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="fed77-163">연락처 [Brightspace by Desire2Learn 지원 팀](https://www.d2l.com/contact/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) tooget these values.</span></span>
 


4. <span data-ttu-id="fed77-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_certificate.png) 

5. <span data-ttu-id="fed77-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fed77-168">tooconfigure single sign on에서 **Brightspace by Desire2Learn** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[Brightspace by Desire2Learn 지원 팀](https://www.d2l.com/contact/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-168">tooconfigure single sign-on on **Brightspace by Desire2Learn** side, you need toosend hello downloaded **Metadata XML** too[Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="fed77-169">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="fed77-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fed77-170">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="fed77-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fed77-171">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fed77-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fed77-172">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="fed77-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="fed77-173">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="fed77-175">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fed77-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fed77-176">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fed77-178">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fed77-180">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fed77-182">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fed77-184">a.</span><span class="sxs-lookup"><span data-stu-id="fed77-184">a.</span></span> <span data-ttu-id="fed77-185">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fed77-186">b.</span><span class="sxs-lookup"><span data-stu-id="fed77-186">b.</span></span> <span data-ttu-id="fed77-187">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fed77-188">c.</span><span class="sxs-lookup"><span data-stu-id="fed77-188">c.</span></span> <span data-ttu-id="fed77-189">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fed77-190">d.</span><span class="sxs-lookup"><span data-stu-id="fed77-190">d.</span></span> <span data-ttu-id="fed77-191">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-191">Click **Create**.</span></span>
 
### <a name="creating-a-brightspace-by-desire2learn-test-user"></a><span data-ttu-id="fed77-192">Brightspace by Desire2Learn 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="fed77-192">Creating a Brightspace by Desire2Learn test user</span></span>

<span data-ttu-id="fed77-193">순서 tooenable Azure AD 사용자가 Brightspace by Desire2Learn에 toolog에서 이러한 해야에 프로 비전 Brightspace by Desire2Learn 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-193">In order tooenable Azure AD users toolog into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="fed77-194">Brightspace by Desire2Learn의 경우 hello hello 사용자 계정을 만들어야 하 여 만든 toobe 프로그램 [Brightspace by Desire2Learn 지원 팀](https://www.d2l.com/contact/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-194">In hello case of Brightspace by Desire2Learn, hello user accounts need toobe created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

>[!NOTE]
><span data-ttu-id="fed77-195">다양 한 Brightspace Desire2Learn 사용자 계정 만들기 도구에서 사용할 수 있습니다 또는 Api에서 제공 Brightspace Desire2Learn tooprovision Azure Active Directory에서 사용자 계정.</span><span class="sxs-lookup"><span data-stu-id="fed77-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fed77-196">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fed77-197">이 섹션에서는 by Desire2Learn tooBrightspace 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBrightspace by Desire2Learn.</span></span>

![사용자 할당][200] 

<span data-ttu-id="fed77-199">**tooassign by Desire2Learn Britta Simon tooBrightspace hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fed77-199">**tooassign Britta Simon tooBrightspace by Desire2Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="fed77-200">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="fed77-202">Hello 응용 프로그램 목록에서 선택 **Brightspace by Desire2Learn**합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-202">In hello applications list, select **Brightspace by Desire2Learn**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_app.png) 

3. <span data-ttu-id="fed77-204">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="fed77-206">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-206">Click **Add** button.</span></span> <span data-ttu-id="fed77-207">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="fed77-209">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fed77-210">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fed77-211">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fed77-212">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="fed77-212">Testing single sign-on</span></span>

<span data-ttu-id="fed77-213">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fed77-214">Hello Brightspace Desire2Learn 타일 hello 액세스 패널에에서 의해을 클릭할 때 자동으로 로그온 tooyour Brightspace Desire2Learn 응용 프로그램에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-214">When you click hello Brightspace by Desire2Learn tile in hello Access Panel, you should get automatically signed-on tooyour Brightspace by Desire2Learn application.</span></span>
<span data-ttu-id="fed77-215">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fed77-215">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fed77-216">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="fed77-216">Additional resources</span></span>

* [<span data-ttu-id="fed77-217">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="fed77-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fed77-218">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="fed77-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_203.png


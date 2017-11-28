---
title: "자습서: Evernote와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Evernote 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="30e23-103">자습서: Evernote와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="30e23-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="30e23-104">이 자습서에 설명 어떻게 toointegrate Evernote Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30e23-104">In this tutorial, you learn how toointegrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30e23-105">다음 이점을 hello로 제공 Evernote Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="30e23-105">Integrating Evernote with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="30e23-106">액세스 tooEvernote을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-106">You can control in Azure AD who has access tooEvernote.</span></span>
- <span data-ttu-id="30e23-107">에 사용자가 tooautomatically get 로그온 tooEvernote (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-107">You can enable your users tooautomatically get signed-on tooEvernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="30e23-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="30e23-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30e23-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="30e23-110">Prerequisites</span></span>

<span data-ttu-id="30e23-111">다음 항목 hello가 필요 tooconfigure Evernote와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-111">tooconfigure Azure AD integration with Evernote, you need hello following items:</span></span>

- <span data-ttu-id="30e23-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="30e23-112">An Azure AD subscription</span></span>
- <span data-ttu-id="30e23-113">Evernote Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="30e23-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="30e23-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="30e23-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="30e23-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="30e23-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="30e23-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30e23-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="30e23-118">Scenario description</span></span>
<span data-ttu-id="30e23-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="30e23-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30e23-121">Evernote는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="30e23-121">Adding Evernote from hello gallery</span></span>
2. <span data-ttu-id="30e23-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="30e23-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-hello-gallery"></a><span data-ttu-id="30e23-123">Evernote는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="30e23-123">Adding Evernote from hello gallery</span></span>
<span data-ttu-id="30e23-124">tooconfigure hello와의 통합 Evernote Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Evernote tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-124">tooconfigure hello integration of Evernote into Azure AD, you need tooadd Evernote from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="30e23-125">**hello 갤러리에서 Evernote tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30e23-125">**tooadd Evernote from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="30e23-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="30e23-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="30e23-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="30e23-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="30e23-133">Hello 검색 상자에 입력 **Evernote**선택, **Evernote** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-133">In hello search box, type **Evernote**, select **Evernote** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evernote hello 결과 목록에서](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="30e23-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="30e23-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="30e23-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Evernote에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="30e23-137">Single sign on toowork에 대 한 Azure AD는 tooknow Evernote에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evernote is tooa user in Azure AD.</span></span> <span data-ttu-id="30e23-138">즉, Azure AD 사용자 및 Evernote에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-138">In other words, a link relationship between an Azure AD user and hello related user in Evernote needs toobe established.</span></span>

<span data-ttu-id="30e23-139">Evernote에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-139">In Evernote, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="30e23-140">tooconfigure 및 Evernote 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-140">tooconfigure and test Azure AD single sign-on with Evernote, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="30e23-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="30e23-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30e23-143">**[Evernote 테스트 사용자 만들기](#create-an-evernote-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Evernote에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - toohave a counterpart of Britta Simon in Evernote that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="30e23-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30e23-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="30e23-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="30e23-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="30e23-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="30e23-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Evernote 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="30e23-148">**tooconfigure Azure AD single sign on, Evernote와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30e23-148">**tooconfigure Azure AD single sign-on with Evernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="30e23-149">Hello hello에 Azure 포털에서에서 **Evernote** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-149">In hello Azure portal, on hello **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="30e23-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="30e23-153">Hello에 **Evernote 도메인 및 Url** 섹션를 hello IDP의 tooconfigure hello 응용 프로그램 시작 모드를 원하는 경우 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-153">On hello **Evernote Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Evernote 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="30e23-155">Hello에 **식별자** textbox hello URL 입력:`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="30e23-155">In hello **Identifier** textbox, type hello URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="30e23-156">확인 **고급 URL 설정 표시** hello tooconfigure hello 응용 프로그램에 필요한 경우 단계를 다음을 수행 하 고 **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="30e23-156">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Evernote 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="30e23-158">Hello에 **로그온 URL** textbox hello URL 입력:`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="30e23-158">In hello **Sign on URL** textbox, type hello URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="30e23-159">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="30e23-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-161">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="30e23-163">Hello에 **Evernote 구성** 섹션에서 클릭 **구성 Evernote** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="30e23-163">On hello **Evernote Configuration** section, click **Configure Evernote** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="30e23-164">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="30e23-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Evernote 구성](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="30e23-166">다른 웹 브라우저 창에서 Evernote 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="30e23-167">너무 이동**' 관리 '**</span><span class="sxs-lookup"><span data-stu-id="30e23-167">Go too**'Admin Console'**</span></span>

    ![관리 콘솔](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="30e23-169">Hello에서 **' 관리 콘솔 '**, 너무 이동**'Security'** 선택 **' Single Sign-on '**</span><span class="sxs-lookup"><span data-stu-id="30e23-169">From hello **'Admin Console'**, go too**‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO 설정](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="30e23-171">다음 값에는 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-171">Configure hello following values:</span></span>

    ![인증서 설정](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="30e23-173">a.</span><span class="sxs-lookup"><span data-stu-id="30e23-173">a.</span></span>  <span data-ttu-id="30e23-174">**SSO 사용:** SSO는 기본적으로 사용 됩니다 (클릭 **사용 하지 않도록 설정할 Single Sign on** tooremove hello SSO 요구 사항)</span><span class="sxs-lookup"><span data-stu-id="30e23-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** tooremove hello SSO requirement)</span></span>

    <span data-ttu-id="30e23-175">b.</span><span class="sxs-lookup"><span data-stu-id="30e23-175">b.</span></span> <span data-ttu-id="30e23-176">붙여넣기 **SAML에서 Single sign-on 서비스 URL** hello에 hello Azure 포털에서에서 복사한 값 **SAML HTTP 요청 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-176">Paste **SAML Single sign-on Service URL** value, which you have copied from hello Azure portal into hello **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="30e23-177">c.</span><span class="sxs-lookup"><span data-stu-id="30e23-177">c.</span></span> <span data-ttu-id="30e23-178">"인증서 시작" 및 "최종 인증서"를 포함 하 여 메모장 및 복사 hello 내용에서 Azure AD에서 hello 다운로드 한 인증서를 열고 hello에 붙여 넣습니다 **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-178">Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into hello **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="30e23-179">d. **변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="30e23-180">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="30e23-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="30e23-181">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="30e23-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="30e23-182">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="30e23-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="30e23-183">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="30e23-183">Create an Azure AD test user</span></span>

<span data-ttu-id="30e23-184">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="30e23-186">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30e23-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="30e23-187">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="30e23-189">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="30e23-191">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="30e23-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="30e23-193">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="30e23-195">a.</span><span class="sxs-lookup"><span data-stu-id="30e23-195">a.</span></span> <span data-ttu-id="30e23-196">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="30e23-197">b.</span><span class="sxs-lookup"><span data-stu-id="30e23-197">b.</span></span> <span data-ttu-id="30e23-198">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="30e23-199">c.</span><span class="sxs-lookup"><span data-stu-id="30e23-199">c.</span></span> <span data-ttu-id="30e23-200">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="30e23-201">d.</span><span class="sxs-lookup"><span data-stu-id="30e23-201">d.</span></span> <span data-ttu-id="30e23-202">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="30e23-203">Evernote 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="30e23-203">Create an Evernote test user</span></span>

<span data-ttu-id="30e23-204">Tooenable Azure AD 사용자가 toolog Evernote로 주문 하 고에 Evernote에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-204">In order tooenable Azure AD users toolog into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="30e23-205">Hello Evernote의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-205">In hello case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="30e23-206">**사용자 계정 수행 tooprovision hello 다음 단계:**</span><span class="sxs-lookup"><span data-stu-id="30e23-206">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="30e23-207">관리자 권한으로 Evernote 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-207">Log in tooyour Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="30e23-208">Hello 클릭 **' 관리 콘솔 '**합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-208">Click hello **'Admin Console'**.</span></span>

    ![관리 콘솔](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="30e23-210">Hello에서 **' 관리 콘솔 '**, 너무 이동**'사용자를 추가'**합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-210">From hello **'Admin Console'**, go too**‘Add users’**.</span></span>

    ![테스트 사용자 추가](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="30e23-212">**팀 멤버 추가** hello에 **전자 메일** textbox 사용자 계정의 hello 전자 메일 주소를 입력 하 고 클릭 **초대 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30e23-212">**Add team members** in hello **Email** textbox, type hello email address of user account and click **Invite.**</span></span>

    ![테스트 사용자 추가](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="30e23-214">을 전달 hello Azure Active Directory 계정 소유자 전자 메일 tooaccept hello 초대를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-214">After invitation is sent, hello Azure Active Directory account holder will receive an email tooaccept hello invitation.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="30e23-215">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="30e23-216">이 섹션에서는 tooEvernote 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvernote.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="30e23-218">**tooassign Britta Simon tooEvernote hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30e23-218">**tooassign Britta Simon tooEvernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="30e23-219">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="30e23-221">Hello 응용 프로그램 목록에서 선택 **Evernote**합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-221">In hello applications list, select **Evernote**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Evernote 링크](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="30e23-223">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="30e23-225">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-225">Click **Add** button.</span></span> <span data-ttu-id="30e23-226">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="30e23-228">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="30e23-229">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="30e23-230">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="30e23-231">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="30e23-231">Test single sign-on</span></span>

<span data-ttu-id="30e23-232">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="30e23-233">Hello 액세스 패널에서에서 hello Evernote 타일을 클릭할 때 로그온 tooyour Evernote 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-233">When you click hello Evernote tile in hello Access Panel, you should get signed-on tooyour Evernote application.</span></span> <span data-ttu-id="30e23-234">개인 계정으로는 조직 계정을 하지만, 그때 필요 toolog로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30e23-234">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="30e23-235">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="30e23-235">Additional resources</span></span>

* [<span data-ttu-id="30e23-236">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="30e23-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30e23-237">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="30e23-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png


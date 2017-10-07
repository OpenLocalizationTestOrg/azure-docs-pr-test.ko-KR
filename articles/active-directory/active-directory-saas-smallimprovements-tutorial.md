---
title: "자습서: Small Improvements와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 개선이 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33213fe4b61f5005cf78bee2c05b2b1e5e71ae8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="cd5a0-103">자습서: Small Improvements와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="cd5a0-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="cd5a0-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 작은 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-104">In this tutorial, you learn how toointegrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd5a0-105">다음 이점을 hello로 제공 개선이 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="cd5a0-105">Integrating Small Improvements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cd5a0-106">Azure ad 액세스 tooSmall 향상 된 기능을 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-106">You can control in Azure AD who has access tooSmall Improvements</span></span>
- <span data-ttu-id="cd5a0-107">프로그램 사용자 tooautomatically get 로그온 tooSmall (Single Sign-on) 기능 향상으로는 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-107">You can enable your users tooautomatically get signed-on tooSmall Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cd5a0-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cd5a0-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd5a0-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cd5a0-110">Prerequisites</span></span>

<span data-ttu-id="cd5a0-111">다음 항목 hello가 필요 tooconfigure 개선이와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-111">tooconfigure Azure AD integration with Small Improvements, you need hello following items:</span></span>

- <span data-ttu-id="cd5a0-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="cd5a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd5a0-113">Small Improvements Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="cd5a0-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cd5a0-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cd5a0-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd5a0-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cd5a0-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cd5a0-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="cd5a0-118">Scenario description</span></span>
<span data-ttu-id="cd5a0-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd5a0-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd5a0-121">Hello 갤러리에서 작은 향상 된 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-121">Adding Small Improvements from hello gallery</span></span>
2. <span data-ttu-id="cd5a0-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="cd5a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-hello-gallery"></a><span data-ttu-id="cd5a0-123">Hello 갤러리에서 작은 향상 된 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-123">Adding Small Improvements from hello gallery</span></span>
<span data-ttu-id="cd5a0-124">tooconfigure hello와의 통합 개선이 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd 개선이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-124">tooconfigure hello integration of Small Improvements into Azure AD, you need tooadd Small Improvements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cd5a0-125">**hello 갤러리에서 개선이 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cd5a0-125">**tooadd Small Improvements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd5a0-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cd5a0-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cd5a0-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="cd5a0-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="cd5a0-133">Hello 검색 상자에 입력 **개선이**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-133">In hello search box, type **Small Improvements**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="cd5a0-135">Hello 결과 패널에서 선택 **개선이**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-135">In hello results panel, select **Small Improvements**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cd5a0-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="cd5a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cd5a0-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Small Improvements에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cd5a0-139">Single sign on toowork에 대 한 Azure AD는 tooknow 작은 향상 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Small Improvements is tooa user in Azure AD.</span></span> <span data-ttu-id="cd5a0-140">즉, Azure AD 사용자 및 작은 향상 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-140">In other words, a link relationship between an Azure AD user and hello related user in Small Improvements needs toobe established.</span></span>

<span data-ttu-id="cd5a0-141">작은 향상 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-141">In Small Improvements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cd5a0-142">tooconfigure 및 작은 향상 된 기능을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-142">tooconfigure and test Azure AD single sign-on with Small Improvements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cd5a0-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cd5a0-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cd5a0-145">**[개선이 테스트 사용자 만들기](#creating-a-small-improvements-test-user)**  -toohave 표현인 연결 된 toohello Azure AD 사용자의 작은 향상 Britta Simon의 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - toohave a counterpart of Britta Simon in Small Improvements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cd5a0-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cd5a0-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cd5a0-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="cd5a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cd5a0-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 개선이 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="cd5a0-150">**tooconfigure Azure AD single sign on 작은 향상 된 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cd5a0-150">**tooconfigure Azure AD single sign-on with Small Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd5a0-151">Hello hello에 Azure 포털에서에서 **개선이** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-151">In hello Azure portal, on hello **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="cd5a0-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="cd5a0-155">Hello에 **작은 향상 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-155">On hello **Small Improvements Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="cd5a0-157">a.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-157">a.</span></span> <span data-ttu-id="cd5a0-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="cd5a0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="cd5a0-159">b.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-159">b.</span></span> <span data-ttu-id="cd5a0-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="cd5a0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd5a0-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-161">These values are not real.</span></span> <span data-ttu-id="cd5a0-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cd5a0-163">연락처 [작은 향상 클라이언트 지원 팀](mailto:support@small-improvements.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="cd5a0-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="cd5a0-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cd5a0-168">Hello에 **작은 향상 된 기능 구성** 섹션에서 클릭 **개선이 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-168">On hello **Small Improvements Configuration** section, click **Configure Small Improvements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cd5a0-169">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="cd5a0-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="cd5a0-171">다른 브라우저 창에서 관리자 권한으로 tooyour 개선이 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-171">In another browser window, sign on tooyour Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="cd5a0-172">Hello 주요 대시보드 페이지에서 클릭 **관리** hello 왼쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-172">From hello main dashboard page, click **Administration** button on hello left.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="cd5a0-174">Hello 클릭 **SAML SSO** 에서 단추 **통합** 섹션.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-174">Click hello **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="cd5a0-176">Hello SSO 설치 페이지에서 다음 단계는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="cd5a0-178">a.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-178">a.</span></span> <span data-ttu-id="cd5a0-179">Hello에 **HTTP 끝점** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-179">In hello **HTTP Endpoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cd5a0-180">b.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-180">b.</span></span> <span data-ttu-id="cd5a0-181">콘텐츠 복사 hello 메모장에서 다운로드 한 인증서를 열고 hello에 붙여 넣습니다 **x509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-181">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="cd5a0-182">c.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-182">c.</span></span> <span data-ttu-id="cd5a0-183">Toohave SSO 및 로그인 폼 인증 옵션 사용자가 원할 경우 다음 hello 확인 **너무 로그인/암호를 통한 액세스를 사용 하도록 설정** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-183">If you wish toohave SSO and Login form authentication option available for users, then check hello **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="cd5a0-184">d.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-184">d.</span></span> <span data-ttu-id="cd5a0-185">Hello에 hello 적절 한 값 tooName hello SSO 로그인 단추 입력 **SAML 프롬프트** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-185">Enter hello appropriate value tooName hello SSO Login button in hello **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="cd5a0-186">e.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-186">e.</span></span> <span data-ttu-id="cd5a0-187">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cd5a0-188">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="cd5a0-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cd5a0-189">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cd5a0-190">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cd5a0-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cd5a0-191">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="cd5a0-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="cd5a0-192">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="cd5a0-194">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cd5a0-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd5a0-195">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cd5a0-197">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cd5a0-199">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cd5a0-201">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cd5a0-203">a.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-203">a.</span></span> <span data-ttu-id="cd5a0-204">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd5a0-205">b.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-205">b.</span></span> <span data-ttu-id="cd5a0-206">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cd5a0-207">c.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-207">c.</span></span> <span data-ttu-id="cd5a0-208">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cd5a0-209">d.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-209">d.</span></span> <span data-ttu-id="cd5a0-210">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="cd5a0-211">Small Improvements 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="cd5a0-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="cd5a0-212">tooenable Azure AD 사용자가 toolog tooSmall 향상 된 기능에에서 이러한 프로 비전 해야 작은 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-212">tooenable Azure AD users toolog in tooSmall Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="cd5a0-213">Hello 개선이의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-213">In hello case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="cd5a0-214">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cd5a0-214">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd5a0-215">관리자 권한으로 로그온 tooyour 개선이 회사 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-215">Sign-on tooyour Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="cd5a0-216">Hello 홈 페이지에서 왼쪽 hello에 toohello 메뉴 이동 **관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-216">From hello Home page, go toohello menu on hello left, click **Administration**.</span></span>

3. <span data-ttu-id="cd5a0-217">Hello 클릭 **사용자 디렉터리** 사용자 관리 섹션에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-217">Click hello **User Directory** button from User Management section.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="cd5a0-219">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-219">Click **Add users**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="cd5a0-221">Hello에 **사용자 추가** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-221">On hello **Add Users** dialog, perform hello following steps:</span></span> 

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="cd5a0-223">a.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-223">a.</span></span> <span data-ttu-id="cd5a0-224">Hello 입력 **이름** 같은 사용자의 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-224">Enter hello **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="cd5a0-225">b.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-225">b.</span></span> <span data-ttu-id="cd5a0-226">Hello 입력 **성** 같은 사용자의 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-226">Enter hello **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="cd5a0-227">c.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-227">c.</span></span> <span data-ttu-id="cd5a0-228">Hello 입력 **전자 메일** 같은 사용자의  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-228">Enter hello **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="cd5a0-229">d.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-229">d.</span></span> <span data-ttu-id="cd5a0-230">Hello에 tooenter hello 개인 메시지를 선택할 수도 있습니다 **알림 전자 메일을 보낼** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-230">You can also choose tooenter hello personal message in hello **Send notification email** box.</span></span> <span data-ttu-id="cd5a0-231">Toosend hello 알림을 않으려면이 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-231">If you do not wish toosend hello notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="cd5a0-232">e.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-232">e.</span></span> <span data-ttu-id="cd5a0-233">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-233">Click **Create Users**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cd5a0-234">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cd5a0-235">이 섹션에서는 Azure에서 single sign-on Britta Simon toouse 사용 하도록 설정 tooSmall 향상 된 기능 액세스를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmall Improvements.</span></span>

![사용자 할당][200] 

<span data-ttu-id="cd5a0-237">**tooassign Britta Simon tooSmall 개선 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cd5a0-237">**tooassign Britta Simon tooSmall Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd5a0-238">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="cd5a0-240">Hello 응용 프로그램 목록에서 선택 **개선이**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-240">In hello applications list, select **Small Improvements**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="cd5a0-242">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="cd5a0-244">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-244">Click **Add** button.</span></span> <span data-ttu-id="cd5a0-245">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="cd5a0-247">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cd5a0-248">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cd5a0-249">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cd5a0-250">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="cd5a0-250">Testing single sign-on</span></span>

<span data-ttu-id="cd5a0-251">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="cd5a0-252">Hello 개선이 hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour 개선이 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd5a0-252">When you click hello Small Improvements tile in hello Access Panel, you should get automatically signed-on tooyour Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cd5a0-253">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="cd5a0-253">Additional resources</span></span>

* [<span data-ttu-id="cd5a0-254">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="cd5a0-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd5a0-255">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="cd5a0-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png


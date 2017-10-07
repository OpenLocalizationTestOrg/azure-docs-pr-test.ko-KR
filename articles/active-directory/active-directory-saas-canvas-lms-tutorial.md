---
title: "자습서: Canvas LMS와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Canvas LMS 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="a0605-103">자습서: Canvas LMS와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a0605-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="a0605-104">이 자습서에 설명 Azure Active Directory (Azure AD)와 toointegrate 캔버스 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-104">In this tutorial, you learn how toointegrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0605-105">Azure AD와 Canvas를 통합 이점을 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="a0605-105">Integrating Canvas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a0605-106">액세스 tooCanvas을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-106">You can control in Azure AD who has access tooCanvas</span></span>
- <span data-ttu-id="a0605-107">프로그램 사용자 tooautomatically get 로그온 tooCanvas (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-107">You can enable your users tooautomatically get signed-on tooCanvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0605-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a0605-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0605-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a0605-110">Prerequisites</span></span>

<span data-ttu-id="a0605-111">캔버스와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-111">tooconfigure Azure AD integration with Canvas, you need hello following items:</span></span>

- <span data-ttu-id="a0605-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a0605-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0605-113">Canvas Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a0605-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0605-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0605-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0605-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a0605-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0605-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0605-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a0605-118">Scenario description</span></span>
<span data-ttu-id="a0605-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0605-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0605-121">캔버스는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="a0605-121">Adding Canvas from hello gallery</span></span>
2. <span data-ttu-id="a0605-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a0605-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-hello-gallery"></a><span data-ttu-id="a0605-123">캔버스는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="a0605-123">Adding Canvas from hello gallery</span></span>
<span data-ttu-id="a0605-124">tooconfigure hello 통합 캔버스의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 캔버스 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-124">tooconfigure hello integration of Canvas into Azure AD, you need tooadd Canvas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a0605-125">**hello 갤러리에서 캔버스 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a0605-125">**tooadd Canvas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0605-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0605-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a0605-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a0605-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a0605-133">Hello 검색 상자에 입력 **캔버스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-133">In hello search box, type **Canvas**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="a0605-135">Hello 결과 패널에서 선택 **캔버스**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-135">In hello results panel, select **Canvas**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0605-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a0605-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a0605-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Canvas에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a0605-139">Single sign on toowork에 대 한 Azure AD는 tooknow 캔버스에 있는 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Canvas is tooa user in Azure AD.</span></span> <span data-ttu-id="a0605-140">즉, Azure AD 사용자 및 hello 캔버스에 있는 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-140">In other words, a link relationship between an Azure AD user and hello related user in Canvas needs toobe established.</span></span>

<span data-ttu-id="a0605-141">캔버스의 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-141">In Canvas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a0605-142">tooconfigure 및 캔버스를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-142">tooconfigure and test Azure AD single sign-on with Canvas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a0605-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a0605-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0605-145">**[캔버스 테스트 사용자 만들기](#creating-a-canvas-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 캔버스에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - toohave a counterpart of Britta Simon in Canvas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0605-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0605-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="a0605-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0605-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a0605-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0605-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 캔버스 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="a0605-150">**tooconfigure Azure AD single sign on 캔버스와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a0605-150">**tooconfigure Azure AD single sign-on with Canvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0605-151">Hello hello에 Azure 포털에서에서 **캔버스** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-151">In hello Azure portal, on hello **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a0605-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="a0605-155">Hello에 **캔버스 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-155">On hello **Canvas Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="a0605-157">a.</span><span class="sxs-lookup"><span data-stu-id="a0605-157">a.</span></span> <span data-ttu-id="a0605-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="a0605-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="a0605-159">b.</span><span class="sxs-lookup"><span data-stu-id="a0605-159">b.</span></span> <span data-ttu-id="a0605-160">Hello에 **식별자** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="a0605-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0605-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-161">These values are not real.</span></span> <span data-ttu-id="a0605-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a0605-163">연락처 [캔버스 클라이언트 지원 팀](https://community.canvaslms.com/community/help) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="a0605-164">Hello에 **SAML 서명 인증서** 섹션을 복사 hello **지문** 인증서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="a0605-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a0605-168">Hello에 **캔버스 구성** 섹션에서 클릭 **구성 캔버스** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="a0605-168">On hello **Canvas Configuration** section, click **Configure Canvas** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a0605-169">복사 hello **암호 변경 URL, 로그 아웃 URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="a0605-169">Copy hello **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="a0605-171">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Canvas 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-171">In a different web browser window, log in tooyour Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="a0605-172">너무 이동**Courses \> 관리 계정 \> Microsoft**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-172">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="a0605-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="a0605-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="a0605-174">Hello hello 왼쪽의 탐색 창에서 선택 **인증**, 클릭 하 고 **새 SAML 구성 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-174">In hello navigation pane on hello left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="a0605-175">![인증](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "인증")</span><span class="sxs-lookup"><span data-stu-id="a0605-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="a0605-176">Hello 현재 통합 페이지에서 다음 단계는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-176">On hello Current Integration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="a0605-177">![현재 통합](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "현재 통합")</span><span class="sxs-lookup"><span data-stu-id="a0605-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="a0605-178">a.</span><span class="sxs-lookup"><span data-stu-id="a0605-178">a.</span></span> <span data-ttu-id="a0605-179">**IdP 엔터티 ID** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-179">In **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a0605-180">b.</span><span class="sxs-lookup"><span data-stu-id="a0605-180">b.</span></span> <span data-ttu-id="a0605-181">**로그온 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-181">In **Log On URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="a0605-182">c.</span><span class="sxs-lookup"><span data-stu-id="a0605-182">c.</span></span> <span data-ttu-id="a0605-183">**로그 아웃 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-183">In **Log Out URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a0605-184">d.</span><span class="sxs-lookup"><span data-stu-id="a0605-184">d.</span></span> <span data-ttu-id="a0605-185">**암호 변경 링크** 붙여넣기 hello 값의 텍스트 상자 **암호 변경 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-185">In **Change Password Link** textbox, paste hello value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="a0605-186">e.</span><span class="sxs-lookup"><span data-stu-id="a0605-186">e.</span></span> <span data-ttu-id="a0605-187">**인증서 지문** 텍스트 붙여넣기 hello **지문** Azure 포털에서 복사 하는 인증서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-187">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="a0605-188">f.</span><span class="sxs-lookup"><span data-stu-id="a0605-188">f.</span></span> <span data-ttu-id="a0605-189">Hello에서 **로그인 특성** 목록에서 **NameID**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-189">From hello **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="a0605-190">g.</span><span class="sxs-lookup"><span data-stu-id="a0605-190">g.</span></span> <span data-ttu-id="a0605-191">Hello에서 **식별자 형식** 목록에서 **emailAddress**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-191">From hello **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="a0605-192">h.</span><span class="sxs-lookup"><span data-stu-id="a0605-192">h.</span></span> <span data-ttu-id="a0605-193">**인증 설정 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="a0605-194">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="a0605-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a0605-195">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="a0605-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a0605-196">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a0605-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0605-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a0605-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="a0605-198">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a0605-200">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a0605-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0605-201">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0605-203">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0605-205">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0605-207">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0605-209">a.</span><span class="sxs-lookup"><span data-stu-id="a0605-209">a.</span></span> <span data-ttu-id="a0605-210">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0605-211">b.</span><span class="sxs-lookup"><span data-stu-id="a0605-211">b.</span></span> <span data-ttu-id="a0605-212">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0605-213">c.</span><span class="sxs-lookup"><span data-stu-id="a0605-213">c.</span></span> <span data-ttu-id="a0605-214">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a0605-215">d.</span><span class="sxs-lookup"><span data-stu-id="a0605-215">d.</span></span> <span data-ttu-id="a0605-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="a0605-217">Canvas 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a0605-217">Creating a Canvas test user</span></span>

<span data-ttu-id="a0605-218">tooenable Azure AD 사용자가 toolog tooCanvas에서 이러한 해야에 프로 비전 캔버스입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-218">tooenable Azure AD users toolog in tooCanvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="a0605-219">Canvas의 경우 사용자 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="a0605-220">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a0605-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0605-221">Tooyour 로그인 **캔버스** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-221">Log in tooyour **Canvas** tenant.</span></span>

2. <span data-ttu-id="a0605-222">너무 이동**Courses \> 관리 계정 \> Microsoft**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-222">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="a0605-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="a0605-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="a0605-224">**사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-224">Click **Users**.</span></span>
   
   <span data-ttu-id="a0605-225">![사용자](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="a0605-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="a0605-226">**새 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="a0605-227">![사용자](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="a0605-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="a0605-228">새 사용자 대화 상자 페이지 추가 hello hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-228">On hello Add a New User dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="a0605-229">![사용자 추가](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="a0605-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="a0605-230">a.</span><span class="sxs-lookup"><span data-stu-id="a0605-230">a.</span></span> <span data-ttu-id="a0605-231">Hello에 **전체 이름을** 텍스트 상자와 같은 사용자의 hello 이름을 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-231">In hello **Full Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="a0605-232">b.</span><span class="sxs-lookup"><span data-stu-id="a0605-232">b.</span></span> <span data-ttu-id="a0605-233">Hello에 **전자 메일** 텍스트 상자와 같은 사용자의 전자 메일을 hello 입력  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-233">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="a0605-234">c.</span><span class="sxs-lookup"><span data-stu-id="a0605-234">c.</span></span> <span data-ttu-id="a0605-235">Hello에 **로그인** 텍스트 상자 같은 hello 사용자의 Azure AD 메일 주소를 입력  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-235">In hello **Login** textbox, enter hello user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="a0605-236">d.</span><span class="sxs-lookup"><span data-stu-id="a0605-236">d.</span></span> <span data-ttu-id="a0605-237">선택 **이 계정 만들기에 대 한 전자 메일 hello 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-237">Select **Email hello user about this account creation**.</span></span>

   <span data-ttu-id="a0605-238">e.</span><span class="sxs-lookup"><span data-stu-id="a0605-238">e.</span></span> <span data-ttu-id="a0605-239">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="a0605-240">다른 Canvas 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 캔버스 tooprovision에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-240">You can use any other Canvas user account creation tools or APIs provided by Canvas tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a0605-241">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a0605-242">이 섹션에서는 tooCanvas 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCanvas.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a0605-244">**tooassign Britta Simon tooCanvas hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a0605-244">**tooassign Britta Simon tooCanvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0605-245">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a0605-247">Hello 응용 프로그램 목록에서 선택 **캔버스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-247">In hello applications list, select **Canvas**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="a0605-249">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a0605-251">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-251">Click **Add** button.</span></span> <span data-ttu-id="a0605-252">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a0605-254">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a0605-255">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0605-256">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0605-257">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a0605-257">Testing single sign-on</span></span>

<span data-ttu-id="a0605-258">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a0605-259">Hello 액세스 패널에서에서 hello 캔버스 타일을 클릭할 때 자동으로 로그온 tooyour 캔버스 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-259">When you click hello Canvas tile in hello Access Panel, you should get automatically signed-on tooyour Canvas application.</span></span>
<span data-ttu-id="a0605-260">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0605-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0605-261">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a0605-261">Additional resources</span></span>

* [<span data-ttu-id="a0605-262">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="a0605-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0605-263">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a0605-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png


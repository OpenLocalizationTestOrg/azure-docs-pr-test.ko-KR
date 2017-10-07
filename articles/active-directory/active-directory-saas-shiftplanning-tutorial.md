---
title: "자습서: Humanity와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 인류 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="14498-103">자습서: Azure Active Directory와 Humanity 통합</span><span class="sxs-lookup"><span data-stu-id="14498-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="14498-104">이 자습서에 설명 어떻게 toointegrate 인류 Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="14498-104">In this tutorial, you learn how toointegrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14498-105">이점 다음 hello로 제공 인류 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="14498-105">Integrating Humanity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="14498-106">액세스 tooHumanity을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14498-106">You can control in Azure AD who has access tooHumanity</span></span>
- <span data-ttu-id="14498-107">프로그램 사용자 tooautomatically get 로그온 tooHumanity (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14498-107">You can enable your users tooautomatically get signed-on tooHumanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="14498-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14498-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="14498-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14498-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="14498-110">Prerequisites</span></span>

<span data-ttu-id="14498-111">인류와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-111">tooconfigure Azure AD integration with Humanity, you need hello following items:</span></span>

- <span data-ttu-id="14498-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="14498-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14498-113">Humanity Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="14498-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14498-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14498-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14498-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="14498-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14498-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14498-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14498-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="14498-118">Scenario description</span></span>
<span data-ttu-id="14498-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14498-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14498-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14498-121">인류는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="14498-121">Adding Humanity from hello gallery</span></span>
2. <span data-ttu-id="14498-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="14498-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-hello-gallery"></a><span data-ttu-id="14498-123">인류는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="14498-123">Adding Humanity from hello gallery</span></span>
<span data-ttu-id="14498-124">Azure AD로 인간성 tooconfigure hello 통합을 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 인류 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-124">tooconfigure hello integration of Humanity into Azure AD, you need tooadd Humanity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="14498-125">**hello 갤러리에서 인류 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="14498-125">**tooadd Humanity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="14498-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="14498-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="14498-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="14498-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="14498-133">Hello 검색 상자에 입력 **인류**합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-133">In hello search box, type **Humanity**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="14498-135">Hello 결과 패널에서 선택 **인류**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-135">In hello results panel, select **Humanity**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="14498-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="14498-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="14498-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Humanity에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="14498-139">Single sign on toowork에 대 한 Azure AD는 tooknow 인간성에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Humanity is tooa user in Azure AD.</span></span> <span data-ttu-id="14498-140">즉, Azure AD 사용자 및 인간성에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-140">In other words, a link relationship between an Azure AD user and hello related user in Humanity needs toobe established.</span></span>

<span data-ttu-id="14498-141">인간성에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-141">In Humanity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="14498-142">tooconfigure 및 인류를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-142">tooconfigure and test Azure AD single sign-on with Humanity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="14498-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="14498-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="14498-145">**[인류 테스트 사용자 만들기](#creating-a-humanity-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 인간성에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - toohave a counterpart of Britta Simon in Humanity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="14498-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="14498-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="14498-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="14498-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="14498-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="14498-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 인류 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="14498-150">**tooconfigure Azure AD single sign on 인류와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="14498-150">**tooconfigure Azure AD single sign-on with Humanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="14498-151">Hello hello에 Azure 포털에서에서 **인류** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-151">In hello Azure portal, on hello **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="14498-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="14498-155">Hello에 **인류 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-155">On hello **Humanity Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="14498-157">a.</span><span class="sxs-lookup"><span data-stu-id="14498-157">a.</span></span> <span data-ttu-id="14498-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="14498-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="14498-159">b.</span><span class="sxs-lookup"><span data-stu-id="14498-159">b.</span></span> <span data-ttu-id="14498-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="14498-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="14498-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="14498-161">These values are not real.</span></span> <span data-ttu-id="14498-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="14498-163">연락처 [인류 클라이언트 지원 팀](https://www.humanity.com/support/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-163">Contact [Humanity Client support team](https://www.humanity.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="14498-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="14498-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="14498-168">Hello에 **인류 구성** 섹션에서 클릭 **구성 인류** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="14498-168">On hello **Humanity Configuration** section, click **Configure Humanity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="14498-169">복사 hello **SAML Single Sign-on 서비스 URL, 및 Sign-Out URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="14498-169">Copy hello **SAML Single Sign-On Service URL, and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="14498-171">다른 웹 브라우저 창에서 tooyour에 로그인 **인류** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-171">In a different web browser window, log in tooyour **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="14498-172">Hello 메뉴에서 hello 위에 표시를 클릭 **Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="14498-173">![관리자](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="14498-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="14498-174">**통합** 아래에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="14498-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="14498-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="14498-176">Hello에 **Single Sign On** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-176">In hello **Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="14498-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="14498-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="14498-178">a.</span><span class="sxs-lookup"><span data-stu-id="14498-178">a.</span></span> <span data-ttu-id="14498-179">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="14498-180">b.</span><span class="sxs-lookup"><span data-stu-id="14498-180">b.</span></span> <span data-ttu-id="14498-181">**암호 로그인 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="14498-182">c.</span><span class="sxs-lookup"><span data-stu-id="14498-182">c.</span></span> <span data-ttu-id="14498-183">붙여넣기 hello **SAML Single Sign-on 서비스 URL** hello에 값 **SAML 발급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="14498-183">Paste hello **SAML Single Sign-On Service URL** value into hello **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="14498-184">d.</span><span class="sxs-lookup"><span data-stu-id="14498-184">d.</span></span> <span data-ttu-id="14498-185">붙여넣기 hello **Sign-Out URL** hello에 값 **원격 로그 아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="14498-185">Paste hello **Sign-Out URL** value into hello **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="14498-186">e.</span><span class="sxs-lookup"><span data-stu-id="14498-186">e.</span></span> <span data-ttu-id="14498-187">콘텐츠를 클립보드에 복사 hello 메모장에서 e-64로 인코딩된 인증서를 열고 toohello 붙여 **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="14498-187">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="14498-188">**설정 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="14498-189">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="14498-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="14498-190">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="14498-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="14498-191">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="14498-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="14498-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="14498-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="14498-193">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="14498-195">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="14498-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="14498-196">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="14498-198">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="14498-200">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="14498-202">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="14498-204">a.</span><span class="sxs-lookup"><span data-stu-id="14498-204">a.</span></span> <span data-ttu-id="14498-205">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14498-206">b.</span><span class="sxs-lookup"><span data-stu-id="14498-206">b.</span></span> <span data-ttu-id="14498-207">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="14498-208">c.</span><span class="sxs-lookup"><span data-stu-id="14498-208">c.</span></span> <span data-ttu-id="14498-209">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="14498-210">d.</span><span class="sxs-lookup"><span data-stu-id="14498-210">d.</span></span> <span data-ttu-id="14498-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="14498-212">Humanity 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="14498-212">Creating a Humanity test user</span></span>

<span data-ttu-id="14498-213">Tooenable Azure AD 사용자가 toolog tooHumanity에 주문 하 고에 인류에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-213">In order tooenable Azure AD users toolog in tooHumanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="14498-214">인간성 hello 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-214">In hello case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="14498-215">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="14498-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="14498-216">Tooyour 로그인 **인류** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-216">Log in tooyour **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="14498-217">**Admin**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="14498-218">![관리자](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="14498-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="14498-219">**Staff**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="14498-220">![직원](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "직원")</span><span class="sxs-lookup"><span data-stu-id="14498-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="14498-221">**작업** 아래에서 **직원 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="14498-222">![직원 추가](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "직원 추가")</span><span class="sxs-lookup"><span data-stu-id="14498-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="14498-223">Hello에 **직원 추가** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-223">In hello **Add Employees** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="14498-224">![직원 저장](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "직원 저장")</span><span class="sxs-lookup"><span data-stu-id="14498-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="14498-225">a.</span><span class="sxs-lookup"><span data-stu-id="14498-225">a.</span></span> <span data-ttu-id="14498-226">형식 hello **이름**, **성**, 및 **전자 메일** 의 hello에 tooprovision 하려는 유효한 AAD 계정의 관련 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-226">Type hello **First Name**, **Last Name**, and **Email** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="14498-227">b.</span><span class="sxs-lookup"><span data-stu-id="14498-227">b.</span></span> <span data-ttu-id="14498-228">**직원 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="14498-229">다른 인류 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 인류 tooprovision에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="14498-229">You can use any other Humanity user account creation tools or APIs provided by Humanity tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="14498-230">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="14498-231">이 섹션에서는 tooHumanity 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHumanity.</span></span>

![사용자 할당][200] 

<span data-ttu-id="14498-233">**tooassign Britta Simon tooHumanity hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="14498-233">**tooassign Britta Simon tooHumanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="14498-234">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="14498-236">Hello 응용 프로그램 목록에서 선택 **인류**합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-236">In hello applications list, select **Humanity**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="14498-238">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="14498-240">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-240">Click **Add** button.</span></span> <span data-ttu-id="14498-241">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="14498-243">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14498-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="14498-244">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="14498-245">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="14498-246">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="14498-246">Testing single sign-on</span></span>

<span data-ttu-id="14498-247">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14498-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="14498-248">Hello 액세스 패널에서에서 hello 인류 타일을 클릭할 때 자동으로 로그온 tooyour 인류 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-248">When you click hello Humanity tile in hello Access Panel, you should get automatically signed-on tooyour Humanity application.</span></span>
<span data-ttu-id="14498-249">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="14498-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14498-250">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="14498-250">Additional resources</span></span>

* [<span data-ttu-id="14498-251">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="14498-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14498-252">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="14498-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png


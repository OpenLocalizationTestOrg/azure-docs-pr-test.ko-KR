---
title: "자습서: RFPIO와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 RFPIO 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="fac9e-103">자습서: RFPIO와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="fac9e-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="fac9e-104">이 자습서에 설명 어떻게 toointegrate RFPIO Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fac9e-104">In this tutorial, you learn how toointegrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fac9e-105">다음 이점을 hello로 제공 RFPIO Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="fac9e-105">Integrating RFPIO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fac9e-106">액세스 tooRFPIO을 지닌 Azure AD에서 사용자를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-106">You can control who in Azure AD who has access tooRFPIO.</span></span>
- <span data-ttu-id="fac9e-107">에 사용자가 tooautomatically get 로그온 tooRFPIO (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-107">You can enable your users tooautomatically get signed-on tooRFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fac9e-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="fac9e-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fac9e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fac9e-110">Prerequisites</span></span>

<span data-ttu-id="fac9e-111">다음 항목 hello가 필요 tooconfigure RFPIO와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-111">tooconfigure Azure AD integration with RFPIO, you need hello following items:</span></span>

- <span data-ttu-id="fac9e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="fac9e-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="fac9e-113">RFPIO Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="fac9e-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="fac9e-114">이 자습서에서는 프로덕션 환경 tootest hello 단계를 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-114">We don't recommend that you use a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="fac9e-115">이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="fac9e-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="fac9e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="fac9e-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="fac9e-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fac9e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="fac9e-118">Scenario description</span></span>
<span data-ttu-id="fac9e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fac9e-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-120">hello scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fac9e-121">Hello 갤러리에서 RFPIO를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-121">Adding RFPIO from hello gallery.</span></span>
2. <span data-ttu-id="fac9e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="fac9e-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-hello-gallery"></a><span data-ttu-id="fac9e-123">RFPIO hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="fac9e-123">Add RFPIO from hello gallery</span></span>
<span data-ttu-id="fac9e-124">tooconfigure hello와의 통합 RFPIO Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 RFPIO tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-124">tooconfigure hello integration of RFPIO into Azure AD, you need tooadd RFPIO from hello gallery tooyour list of managed SaaS apps.</span></span>

### <a name="tooadd-rfpio-from-hello-gallery"></a><span data-ttu-id="fac9e-125">tooadd RFPIO hello 갤러리에서</span><span class="sxs-lookup"><span data-stu-id="fac9e-125">tooadd RFPIO from hello gallery</span></span>

1. <span data-ttu-id="fac9e-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 창의 hello, hello 선택 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fac9e-128">**엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="fac9e-130">tooadd 새 응용 프로그램을 선택 하는 hello **새 응용 프로그램** hello 대화 상자 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-130">tooadd a new application, select hello **New application** button on hello top of dialog box.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="fac9e-132">Hello 검색 상자에 입력 **RFPIO**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-132">In hello search box, type **RFPIO**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="fac9e-134">Hello 결과 패널에서 선택 **RFPIO**를 선택한 후 hello **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-134">In hello results panel, select **RFPIO**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fac9e-136">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="fac9e-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="fac9e-137">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 RFPIO에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fac9e-138">Single sign on toowork에 대 한 Azure AD는 tooknow RFPIO에서 테이블에 해당 사용자와 Azure AD에서 사용자 간에 어떤 hello 관계는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-138">For single sign-on toowork, Azure AD needs tooknow what hello relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="fac9e-139">즉, Azure AD 사용자 및 RFPIO에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-139">In other words, a link relationship between an Azure AD user and hello related user in RFPIO needs toobe established.</span></span>

<span data-ttu-id="fac9e-140">RFPIO에서 hello 값을 할당 **사용자 이름** 의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-140">In RFPIO, assign hello value of **user name** in Azure AD as hello value of  **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fac9e-141">tooconfigure 및 RFPIO 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-141">tooconfigure and test Azure AD single sign-on with RFPIO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fac9e-142">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**-tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fac9e-143">**[Azure AD 테스트를 만들고](#creating-an-azure-ad-test-user)**-Britta Simon와 Azure AD에서 single sign-on tootest 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fac9e-144">**[RFPIO 테스트 사용자 만들기](#creating-a-rfpio-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 RFPIO에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --toohave a counterpart of Britta Simon in RFPIO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fac9e-145">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**-tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-145">**[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fac9e-146">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify hello 구성이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-146">**[Test Single Sign-On](#testing-single-sign-on)** --tooverify if hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fac9e-147">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="fac9e-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fac9e-148">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 RFPIO 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="fac9e-149">**tooconfigure Azure AD single sign on, RFPIO와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fac9e-149">**tooconfigure Azure AD single sign-on with RFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="fac9e-150">Hello hello에 Azure 포털에서에서 **RFPIO** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-150">In hello Azure portal, on hello **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="fac9e-152">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="fac9e-154">Hello에 **RFPIO 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="fac9e-154">On hello **RFPIO Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="fac9e-156">a.</span><span class="sxs-lookup"><span data-stu-id="fac9e-156">a.</span></span> <span data-ttu-id="fac9e-157">Hello에 **식별자** textbox hello URL 입력:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="fac9e-157">In hello **Identifier** textbox, type hello URL: `https://www.rfpio.com`</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="fac9e-159">b.</span><span class="sxs-lookup"><span data-stu-id="fac9e-159">b.</span></span> <span data-ttu-id="fac9e-160">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="fac9e-161">c.</span><span class="sxs-lookup"><span data-stu-id="fac9e-161">c.</span></span> <span data-ttu-id="fac9e-162">Hello에 **릴레이 상태** 텍스트 상자에 문자열 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-162">In hello **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="fac9e-163">연락처 [RFPIO 지원 팀](https://www.rfpio.com/contact/) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) tooget this value.</span></span> 

4. <span data-ttu-id="fac9e-164">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="fac9e-165">Tooconfigure hello 응용 프로그램에 필요한 경우 **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="fac9e-165">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>   

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="fac9e-167">Hello에 **로그온 URL** textbox hello URL 입력:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="fac9e-167">In hello **Sign on URL** textbox, type hello URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="fac9e-168">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="fac9e-170">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-170">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="fac9e-172">로그인 toohello 다른 웹 브라우저 창에서 **RFPIO** 관리자 권한으로 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-172">In a different web browser window, login toohello **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="fac9e-173">Hello 하단 왼쪽된 모서리 드롭다운을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-173">Click on hello bottom left corner dropdown.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="fac9e-175">Hello 클릭 **조직 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-175">Click on hello **Organization Settings**.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="fac9e-177">Hello 클릭 **기능 및 통합**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-177">Click on hello **FEATURES & INTEGRATION**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="fac9e-179">Hello에 **SAML SSO 구성** 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-179">In hello **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="fac9e-181">이 섹션에서 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-181">In this Section perform following actions:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="fac9e-183">a.</span><span class="sxs-lookup"><span data-stu-id="fac9e-183">a.</span></span> <span data-ttu-id="fac9e-184">Hello의 hello 콘텐츠 복사 **다운로드 한 메타 데이터 XML** hello에 붙여 넣습니다 **id 구성** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-184">Copy hello content of hello **Downloaded Metadata XML** and paste it into hello **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="fac9e-185">toocopy hello의 콘텐츠 다운로드 **메타 데이터 XML** 사용 **메모장 + +** 또는 적절 한 **XML 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-185">toocopy hello content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="fac9e-186">b.</span><span class="sxs-lookup"><span data-stu-id="fac9e-186">b.</span></span> <span data-ttu-id="fac9e-187">**유효성 검사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-187">Click **Validate**.</span></span>

    <span data-ttu-id="fac9e-188">c.</span><span class="sxs-lookup"><span data-stu-id="fac9e-188">c.</span></span> <span data-ttu-id="fac9e-189">클릭 한 후 **유효성 검사**플립, **SAML(Enabled)** tooon 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-189">After Clicking **Validate**, Flip **SAML(Enabled)** tooon.</span></span>

    <span data-ttu-id="fac9e-190">d.</span><span class="sxs-lookup"><span data-stu-id="fac9e-190">d.</span></span> <span data-ttu-id="fac9e-191">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="fac9e-192">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="fac9e-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fac9e-193">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="fac9e-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fac9e-194">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fac9e-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fac9e-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="fac9e-195">Create an Azure AD test user</span></span>
<span data-ttu-id="fac9e-196">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="fac9e-198">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fac9e-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fac9e-199">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fac9e-201">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fac9e-203">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fac9e-205">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fac9e-207">a.</span><span class="sxs-lookup"><span data-stu-id="fac9e-207">a.</span></span> <span data-ttu-id="fac9e-208">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fac9e-209">b.</span><span class="sxs-lookup"><span data-stu-id="fac9e-209">b.</span></span> <span data-ttu-id="fac9e-210">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fac9e-211">c.</span><span class="sxs-lookup"><span data-stu-id="fac9e-211">c.</span></span> <span data-ttu-id="fac9e-212">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fac9e-213">d.</span><span class="sxs-lookup"><span data-stu-id="fac9e-213">d.</span></span> <span data-ttu-id="fac9e-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="fac9e-215">RFPIO 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="fac9e-215">Create a RFPIO test user</span></span>

<span data-ttu-id="fac9e-216">tooenable Azure AD 사용자가 toolog tooRFPIO에서 이러한 해야에 프로 비전 RFPIO 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-216">tooenable Azure AD users toolog in tooRFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="fac9e-217">Hello RFPIO의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-217">In hello case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="fac9e-218">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fac9e-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="fac9e-219">관리자 권한으로 RFPIO 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-219">Log in tooyour RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="fac9e-220">Hello 하단 왼쪽된 모서리 드롭다운을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-220">Click on hello bottom left corner dropdown.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="fac9e-222">Hello 클릭 **조직 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-222">Click on hello **Organization Settings**.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="fac9e-224">**TEAM MEMBERS**(팀 멤버)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-224">Click **TEAM MEMBERS**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="fac9e-226">**멤버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-226">Click on **ADD MEMBERS**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="fac9e-228">Hello에 **새 멤버 추가** 섹션.</span><span class="sxs-lookup"><span data-stu-id="fac9e-228">In hello **Add New Members** section.</span></span> <span data-ttu-id="fac9e-229">다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-229">Perform following actions:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="fac9e-231">a.</span><span class="sxs-lookup"><span data-stu-id="fac9e-231">a.</span></span> <span data-ttu-id="fac9e-232">Enter **전자 메일 주소** hello에 **줄당 하나의 전자 메일을 입력** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-232">Enter **Email address** in hello **Enter one email per line** field.</span></span>

    <span data-ttu-id="fac9e-233">b.</span><span class="sxs-lookup"><span data-stu-id="fac9e-233">b.</span></span> <span data-ttu-id="fac9e-234">요구 사항에 따라 **역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="fac9e-235">c.</span><span class="sxs-lookup"><span data-stu-id="fac9e-235">c.</span></span> <span data-ttu-id="fac9e-236">**멤버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="fac9e-237">hello Azure Active Directory 계정 소유자는 전자 메일을 수신 하을 따라 활성화 링크 tooconfirm 자신의 계정의 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-237">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fac9e-238">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fac9e-239">이 섹션에서는 tooRFPIO 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRFPIO.</span></span>

![사용자 할당][200] 

<span data-ttu-id="fac9e-241">**tooassign Britta Simon tooRFPIO hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fac9e-241">**tooassign Britta Simon tooRFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="fac9e-242">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="fac9e-244">Hello 응용 프로그램 목록에서 선택 **RFPIO**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-244">In hello applications list, select **RFPIO**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="fac9e-246">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="fac9e-248">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-248">Click **Add** button.</span></span> <span data-ttu-id="fac9e-249">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="fac9e-251">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fac9e-252">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fac9e-253">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fac9e-254">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="fac9e-254">Test single sign-on</span></span>

<span data-ttu-id="fac9e-255">이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD single sign on 구성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-255">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="fac9e-256">Hello RFPIO hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour RFPIO 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-256">When you click hello RFPIO tile in hello Access Panel, you should get automatically signed-on tooyour RFPIO application.</span></span>
<span data-ttu-id="fac9e-257">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fac9e-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fac9e-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="fac9e-258">Additional resources</span></span>

* [<span data-ttu-id="fac9e-259">방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="fac9e-259">List of tutorials about how toointegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fac9e-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="fac9e-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png


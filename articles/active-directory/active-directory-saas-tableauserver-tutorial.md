---
title: "자습서: Tableau Server와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Tableau 서버입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="83ed1-103">자습서: Tableau Server와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="83ed1-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="83ed1-104">이 자습서에 설명 어떻게 toointegrate Tableau 서버와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83ed1-104">In this tutorial, you learn how toointegrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83ed1-105">Tableau 서버를 Azure AD와 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-105">Integrating Tableau Server with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="83ed1-106">서버 액세스 tooTableau 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-106">You can control in Azure AD who has access tooTableau Server</span></span>
- <span data-ttu-id="83ed1-107">에 사용자가 tooautomatically get 로그온 tooTableau (Single Sign-on) 서버와의 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-107">You can enable your users tooautomatically get signed-on tooTableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83ed1-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="83ed1-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83ed1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="83ed1-110">Prerequisites</span></span>

<span data-ttu-id="83ed1-111">Tableau 서버와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-111">tooconfigure Azure AD integration with Tableau Server, you need hello following items:</span></span>

- <span data-ttu-id="83ed1-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="83ed1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83ed1-113">Tableau Server Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="83ed1-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83ed1-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83ed1-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83ed1-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="83ed1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83ed1-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83ed1-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="83ed1-118">Scenario description</span></span>
<span data-ttu-id="83ed1-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83ed1-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83ed1-121">Tableau 서버 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="83ed1-121">Adding Tableau Server from hello gallery</span></span>
2. <span data-ttu-id="83ed1-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="83ed1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-hello-gallery"></a><span data-ttu-id="83ed1-123">Tableau 서버 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="83ed1-123">Adding Tableau Server from hello gallery</span></span>
<span data-ttu-id="83ed1-124">tooconfigure hello와의 통합 Tableau 서버 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Tableau 서버 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-124">tooconfigure hello integration of Tableau Server into Azure AD, you need tooadd Tableau Server from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="83ed1-125">**tooadd hello 갤러리에서 Tableau 서버 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="83ed1-125">**tooadd Tableau Server from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="83ed1-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83ed1-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="83ed1-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="83ed1-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="83ed1-133">Hello 검색 상자에 입력 **Tableau 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-133">In hello search box, type **Tableau Server**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="83ed1-135">Hello 결과 패널에서 선택 **Tableau 서버**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-135">In hello results panel, select **Tableau Server**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83ed1-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="83ed1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83ed1-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Tableau Server에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="83ed1-139">Single sign on toowork에 대 한 Azure AD는 tooknow Tableau 서버에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Server is tooa user in Azure AD.</span></span> <span data-ttu-id="83ed1-140">즉, Azure AD 사용자 및 hello Tableau 서버에서 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Server needs toobe established.</span></span>

<span data-ttu-id="83ed1-141">Tableau 서버에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-141">In Tableau Server, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="83ed1-142">tooconfigure 및 Tableau 서버와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-142">tooconfigure and test Azure AD single sign-on with Tableau Server, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="83ed1-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="83ed1-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83ed1-145">**[Tableau 서버 테스트 사용자 만들기](#creating-a-tableau-server-test-user)**  -toohave Britta Simon Tableau 서버는 사용자의 연결 된 Azure AD toohello 표현에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - toohave a counterpart of Britta Simon in Tableau Server that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="83ed1-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83ed1-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="83ed1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83ed1-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="83ed1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83ed1-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Tableau 서버 응용 프로그램에 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="83ed1-150">**Azure AD tooconfigure single sign on Tableau 서버와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="83ed1-150">**tooconfigure Azure AD single sign-on with Tableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="83ed1-151">Hello hello에 Azure 포털에서에서 **Tableau 서버** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-151">In hello Azure portal, on hello **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="83ed1-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="83ed1-155">Hello에 **Tableau 서버 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-155">On hello **Tableau Server Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="83ed1-157">a.</span><span class="sxs-lookup"><span data-stu-id="83ed1-157">a.</span></span> <span data-ttu-id="83ed1-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="83ed1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="83ed1-159">b.</span><span class="sxs-lookup"><span data-stu-id="83ed1-159">b.</span></span> <span data-ttu-id="83ed1-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="83ed1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="83ed1-161">c.</span><span class="sxs-lookup"><span data-stu-id="83ed1-161">c.</span></span> <span data-ttu-id="83ed1-162">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="83ed1-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="83ed1-163">hello 이전 값이 실제 값.</span><span class="sxs-lookup"><span data-stu-id="83ed1-163">hello preceding values are not real values.</span></span> <span data-ttu-id="83ed1-164">이상에서는 hello 실제 URL 및 hello Tableau 서버 구성 페이지에서 식별자를 가진 hello 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-164">Later, you update hello values with hello actual URL and identifier from hello Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="83ed1-165">Tableau 서버 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-165">Tableau Server application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="83ed1-166">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="83ed1-167">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 **"사용자 특성"** 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="83ed1-167">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="83ed1-168">hello 다음 스크린샷은 hello에 대 한 예제 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-168">hello following screenshot shows an example for hello same.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="83ed1-170">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 위의 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="83ed1-171">특성 이름</span><span class="sxs-lookup"><span data-stu-id="83ed1-171">Attribute Name</span></span> | <span data-ttu-id="83ed1-172">특성 값</span><span class="sxs-lookup"><span data-stu-id="83ed1-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="83ed1-173">username</span><span class="sxs-lookup"><span data-stu-id="83ed1-173">username</span></span> | <span data-ttu-id="83ed1-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="83ed1-174">*user.displayname*</span></span> |

    <span data-ttu-id="83ed1-175">a.</span><span class="sxs-lookup"><span data-stu-id="83ed1-175">a.</span></span> <span data-ttu-id="83ed1-176">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="83ed1-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="83ed1-179">b.</span><span class="sxs-lookup"><span data-stu-id="83ed1-179">b.</span></span> <span data-ttu-id="83ed1-180">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="83ed1-181">c.</span><span class="sxs-lookup"><span data-stu-id="83ed1-181">c.</span></span> <span data-ttu-id="83ed1-182">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="83ed1-183">d.</span><span class="sxs-lookup"><span data-stu-id="83ed1-183">d.</span></span> <span data-ttu-id="83ed1-184">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-184">Click **Ok**</span></span>


6. <span data-ttu-id="83ed1-185">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="83ed1-187">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-187">Click **Save** button.</span></span>

    <span data-ttu-id="83ed1-188">![Single Sign-On 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="83ed1-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="83ed1-189">SSO 응용 프로그램에 대해 구성 된 tooget toosign에 tooyour Tableau 서버 테 넌 트 관리자 권한으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-189">tooget SSO configured for your application, you need toosign-on tooyour Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="83ed1-190">a.</span><span class="sxs-lookup"><span data-stu-id="83ed1-190">a.</span></span> <span data-ttu-id="83ed1-191">Hello Tableau 서버 구성에서 클릭 hello **SAML** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-191">In hello Tableau Server configuration, click hello **SAML** tab.</span></span>
  
    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="83ed1-193">b.</span><span class="sxs-lookup"><span data-stu-id="83ed1-193">b.</span></span> <span data-ttu-id="83ed1-194">Hello 확인란 선택 **사용 하 여 SAML single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-194">Select hello checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="83ed1-195">c.</span><span class="sxs-lookup"><span data-stu-id="83ed1-195">c.</span></span> <span data-ttu-id="83ed1-196">URL을 반환 하는 tableau 서버-hello Tableau 서버 사용자가 액세스 하는, http://tableau_server 같은 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-196">Tableau Server return URL—hello URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="83ed1-197">http://localhost 를 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="83ed1-198">후행 슬래시가 있는 URL(예: http://tableau_server/)은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="83ed1-199">복사 **Tableau 서버 URL을 반환** tooAzure AD 붙여 **로그온 URL** 텍스트 상자로 **Tableau 서버 도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="83ed1-199">Copy **Tableau Server return URL** and paste it tooAzure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="83ed1-200">d.</span><span class="sxs-lookup"><span data-stu-id="83ed1-200">d.</span></span> <span data-ttu-id="83ed1-201">SAML 엔터티 ID-hello 엔터티 ID Tableau 서버 설치 toohello IdP를 고유 하 게 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-201">SAML entity ID—hello entity ID uniquely identifies your Tableau Server installation toohello IdP.</span></span> <span data-ttu-id="83ed1-202">입력할 수 Tableau 서버 URL 다시 여기에서 원하는 경우 있지만 없는 toobe Tableau 서버 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-202">You can enter your Tableau Server URL again here, if you like, but it does not have toobe your Tableau Server URL.</span></span> <span data-ttu-id="83ed1-203">복사 **SAML 엔터티 ID** tooAzure AD 붙여 **식별자** 텍스트 상자로 **Tableau 서버 도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="83ed1-203">Copy **SAML entity ID** and paste it tooAzure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="83ed1-204">e.</span><span class="sxs-lookup"><span data-stu-id="83ed1-204">e.</span></span> <span data-ttu-id="83ed1-205">Hello 클릭 **메타 데이터 파일 내보내기** hello 텍스트 편집기 응용 프로그램에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-205">Click hello **Export Metadata File** and open it in hello text editor application.</span></span> <span data-ttu-id="83ed1-206">Http Post 및 인덱스 0 hello URL 복사 어설션 소비자 서비스 URL을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy hello URL.</span></span> <span data-ttu-id="83ed1-207">이제 AD tooAzure 붙여 **회신 URL** 텍스트 상자로 **Tableau 서버 도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="83ed1-207">Now paste it tooAzure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="83ed1-208">f.</span><span class="sxs-lookup"><span data-stu-id="83ed1-208">f.</span></span> <span data-ttu-id="83ed1-209">Azure 포털에서 다운로드 한 페더레이션 메타 데이터 파일을 찾아 다음 hello에 업로드 **SAML Idp 메타 데이터 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in hello **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="83ed1-210">g.</span><span class="sxs-lookup"><span data-stu-id="83ed1-210">g.</span></span> <span data-ttu-id="83ed1-211">Hello 클릭 **확인** hello Tableau 서버 구성 페이지에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-211">Click hello **OK** button in hello Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="83ed1-212">고객 hello Tableau 서버 SAML SSO 구성에 tooupload에 모든 인증서를 있고 hello SSO 흐름에에서는 무시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-212">Customer have tooupload any certificate in hello Tableau Server SAML SSO configuration and it will get ignored in hello SSO flow.</span></span>
    ><span data-ttu-id="83ed1-213">SAML Tableau 서버에서 구성 하는 데 도움이 다음 toothis 문서를 참조 하십시오 필요한 경우 [SAML 구성](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm)합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-213">If you need help configuring SAML on Tableau Server then please refer toothis article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="83ed1-214">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="83ed1-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="83ed1-215">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="83ed1-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="83ed1-216">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="83ed1-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83ed1-217">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="83ed1-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="83ed1-218">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="83ed1-220">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="83ed1-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="83ed1-221">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83ed1-223">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83ed1-225">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83ed1-227">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83ed1-229">a.</span><span class="sxs-lookup"><span data-stu-id="83ed1-229">a.</span></span> <span data-ttu-id="83ed1-230">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83ed1-231">b.</span><span class="sxs-lookup"><span data-stu-id="83ed1-231">b.</span></span> <span data-ttu-id="83ed1-232">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83ed1-233">c.</span><span class="sxs-lookup"><span data-stu-id="83ed1-233">c.</span></span> <span data-ttu-id="83ed1-234">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="83ed1-235">d.</span><span class="sxs-lookup"><span data-stu-id="83ed1-235">d.</span></span> <span data-ttu-id="83ed1-236">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="83ed1-237">Tableau Server 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="83ed1-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="83ed1-238">hello이이 섹션의 목적은 toocreate Britta Simon Tableau 서버에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-238">hello objective of this section is toocreate a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="83ed1-239">Tooprovision hello Tableau 서버에서 모든 hello 사용자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-239">You need tooprovision all hello users in hello Tableau server.</span></span> 

<span data-ttu-id="83ed1-240">Hello 사용자의 해당 사용자 이름에는 hello Azure AD의 사용자 지정 특성에 구성 hello 값과 일치 해야 **username**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-240">That username of hello user should match hello value which you have configured in hello Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="83ed1-241">Hello 통합 매핑 협의 하 여 올바른 hello로 [구성 Azure AD Single Sign-on](#configuring-azure-ad-single-sign-on)합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-241">With hello correct mapping hello integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="83ed1-242">Toocreate 사용자를 수동으로 필요 하면 조직에서 toocontact hello Tableau 서버 관리자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-242">If you need toocreate a user manually, you need toocontact hello Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="83ed1-243">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="83ed1-244">이 섹션에서는 액세스 tooTableau 서버 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Server.</span></span>

![사용자 할당][200] 

<span data-ttu-id="83ed1-246">**tooassign Britta Simon tooTableau 서버 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="83ed1-246">**tooassign Britta Simon tooTableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="83ed1-247">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="83ed1-249">Hello 응용 프로그램 목록에서 선택 **Tableau 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-249">In hello applications list, select **Tableau Server**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="83ed1-251">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="83ed1-253">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-253">Click **Add** button.</span></span> <span data-ttu-id="83ed1-254">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="83ed1-256">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="83ed1-257">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83ed1-258">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83ed1-259">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="83ed1-259">Testing single sign-on</span></span>

<span data-ttu-id="83ed1-260">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="83ed1-261">Hello 액세스 패널에에서 hello Tableau 서버 타일을 클릭할 때 자동으로 로그온 tooyour Tableau 서버 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ed1-261">When you click hello Tableau Server tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Server application.</span></span>
<span data-ttu-id="83ed1-262">액세스 패널에 대한 자세한 내용은 [Azure 시작](https://msdn.microsoft.com/library/dn308586)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83ed1-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="83ed1-263">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="83ed1-263">Additional resources</span></span>

* [<span data-ttu-id="83ed1-264">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="83ed1-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83ed1-265">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="83ed1-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png


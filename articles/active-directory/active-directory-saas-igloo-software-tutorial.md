---
title: "자습서: Igloo Software와 Azure Active Directory 통합| Microsoft Azure"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Igloo Software 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="cae97-103">자습서: Igloo Software와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="cae97-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="cae97-104">이 자습서에 설명 어떻게 toointegrate Igloo Software와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cae97-104">In this tutorial, you learn how toointegrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cae97-105">Azure AD와 Igloo Software 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-105">Integrating Igloo Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cae97-106">Azure ad 액세스 tooIgloo 소프트웨어를 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-106">You can control in Azure AD who has access tooIgloo Software</span></span>
- <span data-ttu-id="cae97-107">프로그램 사용자 tooautomatically get 로그온 tooIgloo (Single Sign-on)는 소프트웨어와는 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-107">You can enable your users tooautomatically get signed-on tooIgloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cae97-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cae97-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cae97-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cae97-110">Prerequisites</span></span>

<span data-ttu-id="cae97-111">Igloo Software와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-111">tooconfigure Azure AD integration with Igloo Software, you need hello following items:</span></span>

- <span data-ttu-id="cae97-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="cae97-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cae97-113">Igloo Software Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="cae97-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cae97-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cae97-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cae97-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cae97-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cae97-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cae97-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="cae97-118">Scenario description</span></span>
<span data-ttu-id="cae97-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cae97-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cae97-121">Igloo Software hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="cae97-121">Adding Igloo Software from hello gallery</span></span>
2. <span data-ttu-id="cae97-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="cae97-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-hello-gallery"></a><span data-ttu-id="cae97-123">Igloo Software hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="cae97-123">Adding Igloo Software from hello gallery</span></span>
<span data-ttu-id="cae97-124">tooconfigure hello와의 통합 Igloo Software Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Igloo Software tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-124">tooconfigure hello integration of Igloo Software into Azure AD, you need tooadd Igloo Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cae97-125">**hello 갤러리에서 Igloo Software tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cae97-125">**tooadd Igloo Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cae97-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cae97-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cae97-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="cae97-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="cae97-133">Hello 검색 상자에 입력 **Igloo Software**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-133">In hello search box, type **Igloo Software**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="cae97-135">Hello 결과 패널에서 선택 **Igloo Software**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-135">In hello results panel, select **Igloo Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cae97-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="cae97-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cae97-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Igloo Software에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cae97-139">Single sign on toowork에 대 한 Azure AD는 tooknow Igloo Software에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Igloo Software is tooa user in Azure AD.</span></span> <span data-ttu-id="cae97-140">즉, Azure AD 사용자와 Igloo Software에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-140">In other words, a link relationship between an Azure AD user and hello related user in Igloo Software needs toobe established.</span></span>

<span data-ttu-id="cae97-141">Igloo Software에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-141">In Igloo Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cae97-142">tooconfigure와 Igloo Software와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-142">tooconfigure and test Azure AD single sign-on with Igloo Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cae97-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cae97-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cae97-145">**[Igloo Software 테스트 사용자 만들기](#creating-an-igloo-software-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Igloo Software에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - toohave a counterpart of Britta Simon in Igloo Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cae97-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cae97-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="cae97-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cae97-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="cae97-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cae97-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Igloo Software 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="cae97-150">**Azure AD tooconfigure single sign on와 Igloo Software hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cae97-150">**tooconfigure Azure AD single sign-on with Igloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="cae97-151">Hello hello에 Azure 포털에서에서 **Igloo Software** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-151">In hello Azure portal, on hello **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="cae97-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="cae97-155">Hello에 **Igloo 소프트웨어 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-155">On hello **Igloo Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="cae97-157">a.</span><span class="sxs-lookup"><span data-stu-id="cae97-157">a.</span></span> <span data-ttu-id="cae97-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="cae97-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="cae97-159">b.</span><span class="sxs-lookup"><span data-stu-id="cae97-159">b.</span></span> <span data-ttu-id="cae97-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="cae97-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="cae97-161">c.</span><span class="sxs-lookup"><span data-stu-id="cae97-161">c.</span></span> <span data-ttu-id="cae97-162">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="cae97-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cae97-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-163">These values are not real.</span></span> <span data-ttu-id="cae97-164">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="cae97-165">연락처 [Igloo 소프트웨어 클라이언트 지원 팀](https://www.igloosoftware.com/services/support) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="cae97-166">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="cae97-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="cae97-170">Hello에 **Igloo 소프트웨어 구성** 섹션에서 클릭 **Igloo Software 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="cae97-170">On hello **Igloo Software Configuration** section, click **Configure Igloo Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cae97-171">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="cae97-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="cae97-173">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Igloo Software 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-173">In a different web browser window, log in tooyour Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="cae97-174">Toohello 이동 **제어판**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-174">Go toohello **Control Panel**.</span></span>
   
     <span data-ttu-id="cae97-175">![제어판](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "제어판")</span><span class="sxs-lookup"><span data-stu-id="cae97-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="cae97-176">Hello에 **구성원** 탭을 클릭 **로그인 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-176">In hello **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="cae97-177">![로그인 설정](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "로그인 설정")</span><span class="sxs-lookup"><span data-stu-id="cae97-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="cae97-178">Hello SAML 구성 섹션에서에서 클릭 **SAML 인증 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-178">In hello SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="cae97-179">![SAML 구성](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML 구성")</span><span class="sxs-lookup"><span data-stu-id="cae97-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="cae97-180">Hello에 **일반 구성** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-180">In hello **General Configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cae97-181">![일반 구성](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "일반 구성")</span><span class="sxs-lookup"><span data-stu-id="cae97-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="cae97-182">a.</span><span class="sxs-lookup"><span data-stu-id="cae97-182">a.</span></span> <span data-ttu-id="cae97-183">Hello에 **연결 이름** textbox 구성에 대 한 사용자 지정 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-183">In hello **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="cae97-184">b.</span><span class="sxs-lookup"><span data-stu-id="cae97-184">b.</span></span> <span data-ttu-id="cae97-185">Hello에 **IdP 로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-185">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="cae97-186">c.</span><span class="sxs-lookup"><span data-stu-id="cae97-186">c.</span></span> <span data-ttu-id="cae97-187">Hello에 **IdP 로그 아웃 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-187">In hello **IdP Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="cae97-188">d.</span><span class="sxs-lookup"><span data-stu-id="cae97-188">d.</span></span> <span data-ttu-id="cae97-189">**로그아웃 응답 및 요청 HTTP 형식**을 **POST**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="cae97-190">e.</span><span class="sxs-lookup"><span data-stu-id="cae97-190">e.</span></span> <span data-ttu-id="cae97-191">Open 프로그램 **base64** 로 인코딩된 인증서 내용을 클립보드의 콘텐츠 복사 hello Azure 포털에서 다운로드 한 메모장에 복사한 후 toohello **공용 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="cae97-192">Hello에 **응답 및 인증 구성**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-192">In hello **Response and Authentication Configuration**, perform hello following steps:</span></span>
    
    <span data-ttu-id="cae97-193">![응답 및 인증 구성](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "응답 및 인증 구성")</span><span class="sxs-lookup"><span data-stu-id="cae97-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="cae97-194">a.</span><span class="sxs-lookup"><span data-stu-id="cae97-194">a.</span></span> <span data-ttu-id="cae97-195">**ID 공급자**로 **Microsoft ADFS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="cae97-196">b.</span><span class="sxs-lookup"><span data-stu-id="cae97-196">b.</span></span> <span data-ttu-id="cae97-197">**ID 형식**으로 **전자 메일 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="cae97-198">c.</span><span class="sxs-lookup"><span data-stu-id="cae97-198">c.</span></span> <span data-ttu-id="cae97-199">Hello에 **전자 메일 특성** 텍스트 상자에 **emailaddress**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-199">In hello **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="cae97-200">d.</span><span class="sxs-lookup"><span data-stu-id="cae97-200">d.</span></span> <span data-ttu-id="cae97-201">Hello에 **First Name 특성** 텍스트 상자에 **givenname**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-201">In hello **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="cae97-202">e.</span><span class="sxs-lookup"><span data-stu-id="cae97-202">e.</span></span> <span data-ttu-id="cae97-203">Hello에 **성 특성** 텍스트 상자에 **surname**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-203">In hello **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="cae97-204">Hello toocomplete hello 구성 단계를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-204">Perform hello following steps toocomplete hello configuration:</span></span>
    
    <span data-ttu-id="cae97-205">![로그인할 때 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "로그인할 때 사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="cae97-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="cae97-206">a.</span><span class="sxs-lookup"><span data-stu-id="cae97-206">a.</span></span> <span data-ttu-id="cae97-207">**로그인할 때 사용자 만들기**에서 **로그인할 때 사이트에 새 사용자 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="cae97-208">b.</span><span class="sxs-lookup"><span data-stu-id="cae97-208">b.</span></span> <span data-ttu-id="cae97-209">**로그인 설정**에서 **"로그인" 화면에서 SAML 단추 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="cae97-210">c.</span><span class="sxs-lookup"><span data-stu-id="cae97-210">c.</span></span> <span data-ttu-id="cae97-211">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cae97-212">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="cae97-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cae97-213">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="cae97-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cae97-214">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cae97-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cae97-215">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="cae97-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="cae97-216">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="cae97-218">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cae97-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cae97-219">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cae97-221">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cae97-223">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cae97-225">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cae97-227">a.</span><span class="sxs-lookup"><span data-stu-id="cae97-227">a.</span></span> <span data-ttu-id="cae97-228">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cae97-229">b.</span><span class="sxs-lookup"><span data-stu-id="cae97-229">b.</span></span> <span data-ttu-id="cae97-230">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cae97-231">c.</span><span class="sxs-lookup"><span data-stu-id="cae97-231">c.</span></span> <span data-ttu-id="cae97-232">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cae97-233">d.</span><span class="sxs-lookup"><span data-stu-id="cae97-233">d.</span></span> <span data-ttu-id="cae97-234">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="cae97-235">Igloo Software 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="cae97-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="cae97-236">하면 tooconfigure 사용자 프로 비전 tooIgloo 소프트웨어에 대 한 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-236">There is no action item for you tooconfigure user provisioning tooIgloo Software.</span></span>  

<span data-ttu-id="cae97-237">할당된 된 사용자 잠그려고 할 때이 toolog에 tooIgloo Igloo Software hello 액세스 패널을 사용 하 여 소프트웨어 hello 사용자의 존재 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-237">When an assigned user tries toolog in tooIgloo Software using hello access panel, Igloo Software checks whether hello user exists.</span></span>  <span data-ttu-id="cae97-238">사용할 수 있는 사용자 계정이 없으면 자동으로 Igloo Software에서 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cae97-239">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cae97-240">이 섹션에서는 액세스 tooIgloo 소프트웨어를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIgloo Software.</span></span>

![사용자 할당][200] 

<span data-ttu-id="cae97-242">**tooassign Britta Simon tooIgloo 소프트웨어 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cae97-242">**tooassign Britta Simon tooIgloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="cae97-243">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="cae97-245">Hello 응용 프로그램 목록에서 선택 **Igloo Software**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-245">In hello applications list, select **Igloo Software**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="cae97-247">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="cae97-249">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-249">Click **Add** button.</span></span> <span data-ttu-id="cae97-250">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="cae97-252">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cae97-253">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cae97-254">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cae97-255">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="cae97-255">Testing single sign-on</span></span>

<span data-ttu-id="cae97-256">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cae97-257">Hello 액세스 패널에서에서 hello Igloo Software 타일을 클릭할 때 자동으로 로그온 tooyour Igloo Software 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-257">When you click hello Igloo Software tile in hello Access Panel, you should get automatically signed-on tooyour Igloo Software application.</span></span>
<span data-ttu-id="cae97-258">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cae97-258">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cae97-259">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="cae97-259">Additional resources</span></span>

* [<span data-ttu-id="cae97-260">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="cae97-260">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cae97-261">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="cae97-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png


---
title: "자습서: Optimizely와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Optimizely 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="02b5e-103">자습서: Optimizely와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="02b5e-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="02b5e-104">이 자습서에 설명 어떻게 toointegrate Optimizely Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02b5e-104">In this tutorial, you learn how toointegrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02b5e-105">다음 이점을 hello로 제공 Optimizely Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="02b5e-105">Integrating Optimizely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="02b5e-106">액세스 tooOptimizely을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-106">You can control in Azure AD who has access tooOptimizely</span></span>
- <span data-ttu-id="02b5e-107">프로그램 사용자 tooautomatically get 로그온 tooOptimizely (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-107">You can enable your users tooautomatically get signed-on tooOptimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="02b5e-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="02b5e-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02b5e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="02b5e-110">Prerequisites</span></span>

<span data-ttu-id="02b5e-111">다음 항목 hello가 필요 tooconfigure Optimizely와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-111">tooconfigure Azure AD integration with Optimizely, you need hello following items:</span></span>

- <span data-ttu-id="02b5e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="02b5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02b5e-113">Optimizely Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="02b5e-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02b5e-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02b5e-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02b5e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="02b5e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="02b5e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02b5e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="02b5e-118">Scenario description</span></span>
<span data-ttu-id="02b5e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="02b5e-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02b5e-121">Optimizely는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="02b5e-121">Adding Optimizely from hello gallery</span></span>
2. <span data-ttu-id="02b5e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="02b5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-hello-gallery"></a><span data-ttu-id="02b5e-123">Optimizely는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="02b5e-123">Adding Optimizely from hello gallery</span></span>
<span data-ttu-id="02b5e-124">tooconfigure hello와의 통합 Optimizely Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Optimizely tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-124">tooconfigure hello integration of Optimizely into Azure AD, you need tooadd Optimizely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="02b5e-125">**hello 갤러리에서 Optimizely tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="02b5e-125">**tooadd Optimizely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="02b5e-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="02b5e-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="02b5e-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="02b5e-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="02b5e-133">Hello 검색 상자에 입력 **Optimizely**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-133">In hello search box, type **Optimizely**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="02b5e-135">Hello 결과 패널에서 선택 **Optimizely**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-135">In hello results panel, select **Optimizely**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="02b5e-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="02b5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="02b5e-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Optimizely에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="02b5e-139">Single sign on toowork에 대 한 Azure AD는 tooknow Optimizely에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Optimizely is tooa user in Azure AD.</span></span> <span data-ttu-id="02b5e-140">즉, Azure AD 사용자 및 Optimizely에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-140">In other words, a link relationship between an Azure AD user and hello related user in Optimizely needs toobe established.</span></span>

<span data-ttu-id="02b5e-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Optimizely에 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Optimizely.</span></span>

<span data-ttu-id="02b5e-142">tooconfigure 및 Optimizely 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-142">tooconfigure and test Azure AD single sign-on with Optimizely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="02b5e-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="02b5e-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02b5e-145">**[Optimizely 테스트 사용자 만들기](#creating-an-optimizely-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Optimizely에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - toohave a counterpart of Britta Simon in Optimizely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="02b5e-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02b5e-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="02b5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="02b5e-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="02b5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="02b5e-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Optimizely 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="02b5e-150">**tooconfigure Azure AD single sign on, Optimizely와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="02b5e-150">**tooconfigure Azure AD single sign-on with Optimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="02b5e-151">Hello hello에 Azure 포털에서에서 **Optimizely** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-151">In hello Azure portal, on hello **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="02b5e-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="02b5e-155">Hello에 **Optimizely 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-155">On hello **Optimizely Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="02b5e-157">a.</span><span class="sxs-lookup"><span data-stu-id="02b5e-157">a.</span></span> <span data-ttu-id="02b5e-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="02b5e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="02b5e-159">b.</span><span class="sxs-lookup"><span data-stu-id="02b5e-159">b.</span></span> <span data-ttu-id="02b5e-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="02b5e-160">In hello **Identifier** textbox, type a URL using hello following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="02b5e-161">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-161">These values are not hello real.</span></span> <span data-ttu-id="02b5e-162">Hello 실제 로그온 URL 및 hello 자습서의 뒷부분에 설명 된 식별자를 가진 hello 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-162">You will update hello value with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="02b5e-163">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-163">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="02b5e-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-165">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="02b5e-167">Hello에 **Optimizely 구성** 섹션에서 클릭 **구성 Optimizely** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="02b5e-167">On hello **Optimizely Configuration** section, click **Configure Optimizely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="02b5e-168">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="02b5e-168">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="02b5e-170">tooconfigure single sign on에서 **Optimizely** 쪽 Optimizely 계정 관리자에 게 문의 하 고, 다운로드 한 hello **인증서 (Base64)**, 및 **SAML Single Sign-on 서비스 URL** .</span><span class="sxs-lookup"><span data-stu-id="02b5e-170">tooconfigure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide hello downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="02b5e-171">응답 tooyour 전자 메일에서 Optimizely 하면 로그온 URL (SP에서 시작한 SSO) hello 및 hello 식별자 (서비스 공급자 엔터티 ID) 값 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-171">In response tooyour email, Optimizely provides you with hello Sign On URL (SP-initiated SSO) and hello Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="02b5e-172">a.</span><span class="sxs-lookup"><span data-stu-id="02b5e-172">a.</span></span> <span data-ttu-id="02b5e-173">복사 hello **SP 시작 SSO URL** Optimizely, 및 붙여넣기 hello에 의해 제공 된 **로그온 URL** 텍스트 상자로 **Optimizely 도메인 및 Url** Azure 포털에서 섹션</span><span class="sxs-lookup"><span data-stu-id="02b5e-173">Copy hello **SP-initiated SSO URL** provided by Optimizely, and paste into hello **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="02b5e-174">b.</span><span class="sxs-lookup"><span data-stu-id="02b5e-174">b.</span></span> <span data-ttu-id="02b5e-175">복사 hello **서비스 공급자 엔터티 ID가** Optimizely, 및 붙여넣기 hello에 의해 제공 된 **식별자** 텍스트 상자로 **Optimizely 도메인 및 Url** Azure 포털에서 섹션</span><span class="sxs-lookup"><span data-stu-id="02b5e-175">Copy hello **Service Provider Entity ID** provided by Optimizely, and paste into hello **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="02b5e-176">다른 브라우저 창에서 로그온 tooyour Optimizely 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-176">In a different browser window, sign-on tooyour Optimizely application.</span></span>

10. <span data-ttu-id="02b5e-177">Hello top에 이름 오른쪽 모서리에 있는 계정을 클릭 한 다음 **계정 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-177">Click you account name in hello top right corner and then **Account Settings**.</span></span>
   
    ![Azure AD Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="02b5e-179">Hello 계정 탭에 확인란 hello **SSO 사용** 에서 Single Sign On hello에 **개요** 섹션.</span><span class="sxs-lookup"><span data-stu-id="02b5e-179">In hello Account tab, check hello box **Enable SSO** under Single Sign On in hello **Overview** section.</span></span>
   
    ![Azure AD Single Sign-On](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="02b5e-181">페이지 맨 아래에 있는 **저장**</span><span class="sxs-lookup"><span data-stu-id="02b5e-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="02b5e-182">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="02b5e-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="02b5e-183">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="02b5e-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="02b5e-184">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="02b5e-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="02b5e-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="02b5e-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="02b5e-186">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="02b5e-188">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="02b5e-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="02b5e-189">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="02b5e-191">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="02b5e-193">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="02b5e-195">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="02b5e-197">a.</span><span class="sxs-lookup"><span data-stu-id="02b5e-197">a.</span></span> <span data-ttu-id="02b5e-198">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02b5e-199">b.</span><span class="sxs-lookup"><span data-stu-id="02b5e-199">b.</span></span> <span data-ttu-id="02b5e-200">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** Britta Simon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="02b5e-201">c.</span><span class="sxs-lookup"><span data-stu-id="02b5e-201">c.</span></span> <span data-ttu-id="02b5e-202">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="02b5e-203">d.</span><span class="sxs-lookup"><span data-stu-id="02b5e-203">d.</span></span> <span data-ttu-id="02b5e-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="02b5e-205">Optimizely 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="02b5e-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="02b5e-206">이 섹션에서는 Optimizely에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="02b5e-207">Hello 홈 페이지에서 선택 **공동 작업자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-207">On hello home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="02b5e-208">tooadd 새 공동 작업자 toohello 프로젝트 클릭 **새 공동 작업자**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-208">tooadd new collaborator toohello project, click **New Collaborator**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="02b5e-210">Hello 전자 메일 주소 입력 한 역할을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-210">Fill in hello email address and assign them a role.</span></span> <span data-ttu-id="02b5e-211">**초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-211">Click **Invite**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="02b5e-213">테스트 사용자는 이메일 초대를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-213">They receive an email invite.</span></span> <span data-ttu-id="02b5e-214">Toolog tooOptimizely에서 권한이 hello 전자 메일 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-214">Using hello email address, they have toolog in tooOptimizely.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="02b5e-215">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="02b5e-216">이 섹션에서는 tooOptimizely 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOptimizely.</span></span>

![사용자 할당][200] 

<span data-ttu-id="02b5e-218">**tooassign Britta Simon tooOptimizely hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="02b5e-218">**tooassign Britta Simon tooOptimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="02b5e-219">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="02b5e-221">Hello 응용 프로그램 목록에서 선택 **Optimizely**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-221">In hello applications list, select **Optimizely**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="02b5e-223">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="02b5e-225">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-225">Click **Add** button.</span></span> <span data-ttu-id="02b5e-226">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="02b5e-228">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="02b5e-229">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02b5e-230">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="02b5e-231">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="02b5e-231">Testing single sign-on</span></span>

<span data-ttu-id="02b5e-232">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="02b5e-233">Hello 액세스 패널에서에서 hello Optimizely 타일을 클릭할 때 자동으로 로그온 tooyour Optimizely 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b5e-233">When you click hello Optimizely tile in hello Access Panel, you should get automatically signed-on tooyour Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="02b5e-234">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="02b5e-234">Additional resources</span></span>

* [<span data-ttu-id="02b5e-235">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="02b5e-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02b5e-236">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="02b5e-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png


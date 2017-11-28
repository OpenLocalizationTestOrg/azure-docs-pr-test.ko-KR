---
title: "자습서: Bonusly와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Bonusly 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="19a33-103">자습서: Bonusly와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="19a33-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="19a33-104">이 자습서에 설명 어떻게 toointegrate Bonusly Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19a33-104">In this tutorial, you learn how toointegrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19a33-105">다음 이점을 hello로 제공 Bonusly Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="19a33-105">Integrating Bonusly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="19a33-106">액세스 tooBonusly을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-106">You can control in Azure AD who has access tooBonusly</span></span>
- <span data-ttu-id="19a33-107">프로그램 사용자 tooautomatically get 로그온 tooBonusly (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-107">You can enable your users tooautomatically get signed-on tooBonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="19a33-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="19a33-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19a33-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="19a33-110">Prerequisites</span></span>

<span data-ttu-id="19a33-111">다음 항목 hello가 필요 tooconfigure Bonusly와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-111">tooconfigure Azure AD integration with Bonusly, you need hello following items:</span></span>

- <span data-ttu-id="19a33-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="19a33-112">An Azure AD subscription</span></span>
- <span data-ttu-id="19a33-113">Bonusly Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="19a33-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="19a33-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="19a33-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19a33-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="19a33-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="19a33-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19a33-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="19a33-118">Scenario description</span></span>
<span data-ttu-id="19a33-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="19a33-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19a33-121">Bonusly는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="19a33-121">Adding Bonusly from hello gallery</span></span>
2. <span data-ttu-id="19a33-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="19a33-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-hello-gallery"></a><span data-ttu-id="19a33-123">Bonusly는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="19a33-123">Adding Bonusly from hello gallery</span></span>
<span data-ttu-id="19a33-124">tooconfigure hello와의 통합 Bonusly Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Bonusly tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-124">tooconfigure hello integration of Bonusly into Azure AD, you need tooadd Bonusly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="19a33-125">**hello 갤러리에서 Bonusly tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="19a33-125">**tooadd Bonusly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="19a33-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="19a33-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="19a33-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="19a33-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="19a33-133">Hello 검색 상자에 입력 **Bonusly**선택, **Bonusly** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-133">In hello search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Bonusly hello 결과 목록에서](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="19a33-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="19a33-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="19a33-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Bonusly에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="19a33-137">Single sign on toowork에 대 한 Azure AD는 tooknow Bonusly에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bonusly is tooa user in Azure AD.</span></span> <span data-ttu-id="19a33-138">즉, Azure AD 사용자 및 Bonusly에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-138">In other words, a link relationship between an Azure AD user and hello related user in Bonusly needs toobe established.</span></span>

<span data-ttu-id="19a33-139">Bonusly에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-139">In Bonusly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="19a33-140">tooconfigure 및 Bonusly 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-140">tooconfigure and test Azure AD single sign-on with Bonusly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="19a33-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="19a33-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19a33-143">**[Bonusly 테스트 사용자 만들기](#create-a-bonusly-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Bonusly에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - toohave a counterpart of Britta Simon in Bonusly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="19a33-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19a33-145">**[Single Sign-on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="19a33-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="19a33-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="19a33-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="19a33-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Bonusly 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="19a33-148">**tooconfigure Azure AD single sign on, Bonusly와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="19a33-148">**tooconfigure Azure AD single sign-on with Bonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="19a33-149">Hello hello에 Azure 포털에서에서 **Bonusly** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-149">In hello Azure portal, on hello **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="19a33-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="19a33-153">Hello에 **Bonusly 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-153">On hello **Bonusly Domain and URLs** section, perform hello following steps:</span></span>

    ![Bonusly 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="19a33-155">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="19a33-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="19a33-156">hello 값이 실제 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-156">hello value is not real.</span></span> <span data-ttu-id="19a33-157">업데이트 hello 값과 실제 회신 URL hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-157">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="19a33-158">연락처 [Bonusly 지원 팀](https://Bonusly/contact) tooget hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-158">Contact [Bonusly support team](https://Bonusly/contact) tooget hello value.</span></span>
 
4. <span data-ttu-id="19a33-159">Hello에 **SAML 서명 인증서** 섹션을 복사 hello **지문** hello 인증서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="19a33-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-161">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="19a33-163">Hello에 **Bonusly 구성** 섹션에서 클릭 **Bonusly 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="19a33-163">On hello **Bonusly Configuration** section, click **Configure Bonusly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="19a33-164">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="19a33-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Bonusly 구성](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="19a33-166">다른 브라우저 창에서 tooyour에 로그인 **Bonusly** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-166">In a different browser window, log in tooyour **Bonusly** tenant.</span></span>

8. <span data-ttu-id="19a33-167">도구 모음의 hello hello 위쪽에 클릭 **설정**를 선택한 후 **통합 및 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-167">In hello toolbar on hello top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="19a33-168">![Bonusly 소셜 섹션](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="19a33-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="19a33-169">**Single Sign-On**에서 **SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="19a33-170">Hello에 **SAML** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-170">On hello **SAML** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="19a33-171">![Bonusly Saml 대화 상자 페이지](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="19a33-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="19a33-172">a.</span><span class="sxs-lookup"><span data-stu-id="19a33-172">a.</span></span> <span data-ttu-id="19a33-173">Hello에 **IdP SSO 대상 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-173">In hello **IdP SSO target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="19a33-174">b.</span><span class="sxs-lookup"><span data-stu-id="19a33-174">b.</span></span> <span data-ttu-id="19a33-175">Hello에 **IdP 발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-175">In hello **IdP Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="19a33-176">c.</span><span class="sxs-lookup"><span data-stu-id="19a33-176">c.</span></span> <span data-ttu-id="19a33-177">Hello에 **IdP 로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-177">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="19a33-178">d.</span><span class="sxs-lookup"><span data-stu-id="19a33-178">d.</span></span> <span data-ttu-id="19a33-179">붙여넣기는 **지문** 값이 hello에 Azure 포털에서 복사 **인증서 지문** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-179">Paste the **Thumbprint** value copied from Azure portal into hello **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="19a33-180">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="19a33-181">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="19a33-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="19a33-182">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="19a33-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="19a33-183">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="19a33-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="19a33-184">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="19a33-184">Create an Azure AD test user</span></span>
<span data-ttu-id="19a33-185">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="19a33-187">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="19a33-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="19a33-188">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="19a33-190">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="19a33-192">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![hello 추가 단추](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="19a33-194">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="19a33-196">a.</span><span class="sxs-lookup"><span data-stu-id="19a33-196">a.</span></span> <span data-ttu-id="19a33-197">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="19a33-198">b.</span><span class="sxs-lookup"><span data-stu-id="19a33-198">b.</span></span> <span data-ttu-id="19a33-199">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="19a33-200">c.</span><span class="sxs-lookup"><span data-stu-id="19a33-200">c.</span></span> <span data-ttu-id="19a33-201">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="19a33-202">d.</span><span class="sxs-lookup"><span data-stu-id="19a33-202">d.</span></span> <span data-ttu-id="19a33-203">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="19a33-204">Bonusly 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="19a33-204">Create a Bonusly test user</span></span>

<span data-ttu-id="19a33-205">Tooenable Azure AD 사용자가 toolog tooBonusly에 주문 하 고에 Bonusly에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-205">In order tooenable Azure AD users toolog in tooBonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="19a33-206">Hello Bonusly의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-206">In hello case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="19a33-207">다른 Bonusly 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Api에서 제공 Bonusly tooprovision AAD 사용자 계정을 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly tooprovision AAD user accounts.</span></span>
>  

<span data-ttu-id="19a33-208">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="19a33-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="19a33-209">웹 브라우저 창에서 tooyour Bonusly 테 넌 트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-209">In a web browser window, log in tooyour Bonusly tenant.</span></span>

2. <span data-ttu-id="19a33-210">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="19a33-211">![설정](./media/active-directory-saas-bonus-tutorial/ic781041.png "설정")</span><span class="sxs-lookup"><span data-stu-id="19a33-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="19a33-212">Hello 클릭 **사용자 및 보너스** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-212">Click hello **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="19a33-213">![사용자 및 보너스](./media/active-directory-saas-bonus-tutorial/ic781042.png "사용자 및 보너스")</span><span class="sxs-lookup"><span data-stu-id="19a33-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="19a33-214">**사용자 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="19a33-215">![사용자 관리](./media/active-directory-saas-bonus-tutorial/ic781043.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="19a33-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="19a33-216">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="19a33-217">![사용자 추가](./media/active-directory-saas-bonus-tutorial/ic781044.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="19a33-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="19a33-218">Hello에 **사용자 추가** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-218">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="19a33-219">![사용자 추가](./media/active-directory-saas-bonus-tutorial/ic781045.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="19a33-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="19a33-220">a.</span><span class="sxs-lookup"><span data-stu-id="19a33-220">a.</span></span> <span data-ttu-id="19a33-221">Hello에 **이름** textbox hello와 같은 사용자의 이름을 입력 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-221">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="19a33-222">b.</span><span class="sxs-lookup"><span data-stu-id="19a33-222">b.</span></span> <span data-ttu-id="19a33-223">Hello에 **성** textbox hello와 같은 사용자의 성을 입력 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-223">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="19a33-224">c.</span><span class="sxs-lookup"><span data-stu-id="19a33-224">c.</span></span> <span data-ttu-id="19a33-225">Hello에 **전자 메일** 텍스트 상자와 같은 사용자의 전자 메일을 hello 입력  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-225">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="19a33-226">d.</span><span class="sxs-lookup"><span data-stu-id="19a33-226">d.</span></span> <span data-ttu-id="19a33-227">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="19a33-228">hello Azure AD 계정 보유자 데이터베이스가 활성화 전에 tooconfirm hello 계정 연결을 포함 하는 전자 메일을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-228">hello Azure AD account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span>
     >  

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="19a33-229">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-229">Assign hello Azure AD test user</span></span>

<span data-ttu-id="19a33-230">이 섹션에서는 tooBonusly 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBonusly.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="19a33-232">**tooassign Britta Simon tooBonusly hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="19a33-232">**tooassign Britta Simon tooBonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="19a33-233">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="19a33-235">Hello 응용 프로그램 목록에서 선택 **Bonusly**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-235">In hello applications list, select **Bonusly**.</span></span>

    ![hello Bonusly hello 응용 프로그램 목록에서 링크](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="19a33-237">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="19a33-239">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-239">Click **Add** button.</span></span> <span data-ttu-id="19a33-240">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="19a33-242">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="19a33-243">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="19a33-244">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="19a33-245">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="19a33-245">Test single sign-on</span></span>

<span data-ttu-id="19a33-246">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="19a33-247">Hello Bonusly 타일을 클릭할 때 hello 액세스 패널에서 자동으로 로그온 tooyour Bonusly 응용 프로그램을 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-247">When you click hello Bonusly tile in hello Access Panel, you should get automatically signed-on tooyour Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19a33-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="19a33-248">Additional resources</span></span>

* [<span data-ttu-id="19a33-249">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="19a33-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19a33-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="19a33-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png


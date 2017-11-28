---
title: "자습서: ThousandEyes와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 ThousandEyes 간에 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="16b11-103">자습서: ThousandEyes와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="16b11-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="16b11-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 ThousandEyes 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-104">In this tutorial, you learn how toointegrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16b11-105">Azure AD와 ThousandEyes 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-105">Integrating ThousandEyes with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="16b11-106">액세스 tooThousandEyes을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-106">You can control in Azure AD who has access tooThousandEyes</span></span>
- <span data-ttu-id="16b11-107">프로그램 사용자 tooautomatically get 로그온 tooThousandEyes (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-107">You can enable your users tooautomatically get signed-on tooThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="16b11-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="16b11-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16b11-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="16b11-110">Prerequisites</span></span>

<span data-ttu-id="16b11-111">ThousandEyes와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-111">tooconfigure Azure AD integration with ThousandEyes, you need hello following items:</span></span>

- <span data-ttu-id="16b11-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="16b11-112">An Azure AD subscription</span></span>
- <span data-ttu-id="16b11-113">ThousandEyes Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="16b11-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16b11-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16b11-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16b11-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="16b11-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="16b11-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16b11-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="16b11-118">Scenario description</span></span>
<span data-ttu-id="16b11-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16b11-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16b11-121">ThousandEyes는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="16b11-121">Adding ThousandEyes from hello gallery</span></span>
2. <span data-ttu-id="16b11-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="16b11-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-hello-gallery"></a><span data-ttu-id="16b11-123">ThousandEyes는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="16b11-123">Adding ThousandEyes from hello gallery</span></span>
<span data-ttu-id="16b11-124">tooconfigure hello와의 통합 ThousandEyes Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 ThousandEyes tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-124">tooconfigure hello integration of ThousandEyes into Azure AD, you need tooadd ThousandEyes from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="16b11-125">**ThousandEyes hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="16b11-125">**tooadd ThousandEyes from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="16b11-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="16b11-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="16b11-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="16b11-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="16b11-133">Hello 검색 상자에 입력 **ThousandEyes**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-133">In hello search box, type **ThousandEyes**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="16b11-135">Hello 결과 패널에서 선택 **ThousandEyes**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-135">In hello results panel, select **ThousandEyes**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="16b11-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="16b11-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="16b11-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 ThousandEyes에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="16b11-139">Single sign on toowork에 대 한 Azure AD는 tooknow ThousandEyes에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThousandEyes is tooa user in Azure AD.</span></span> <span data-ttu-id="16b11-140">즉, Azure AD 사용자와 ThousandEyes에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-140">In other words, a link relationship between an Azure AD user and hello related user in ThousandEyes needs toobe established.</span></span>

<span data-ttu-id="16b11-141">ThousandEyes에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-141">In ThousandEyes, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="16b11-142">tooconfigure와 ThousandEyes 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-142">tooconfigure and test Azure AD single sign-on with ThousandEyes, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="16b11-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="16b11-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16b11-145">**[ThousandEyes 테스트 사용자 만들기](#creating-a-thousandeyes-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 ThousandEyes에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - toohave a counterpart of Britta Simon in ThousandEyes that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="16b11-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16b11-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="16b11-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="16b11-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="16b11-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="16b11-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 ThousandEyes 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="16b11-150">**tooconfigure Azure AD single sign on와 ThousandEyes, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="16b11-150">**tooconfigure Azure AD single sign-on with ThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="16b11-151">Hello hello에 Azure 포털에서에서 **ThousandEyes** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-151">In hello Azure portal, on hello **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="16b11-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="16b11-155">Hello에 **ThousandEyes 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-155">On hello **ThousandEyes Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="16b11-157">Hello에 **로그온 URL** 텍스트 상자에 다음 URL로:`https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="16b11-157">In hello **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="16b11-158">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="16b11-160">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-160">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="16b11-162">Hello에 **ThousandEyes 구성** 섹션에서 클릭 **구성 ThousandEyes** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="16b11-162">On hello **ThousandEyes Configuration** section, click **Configure ThousandEyes** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="16b11-163">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="16b11-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="16b11-165">다른 웹 브라우저 창에서 tooyour 로그인 **ThousandEyes** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-165">In a different web browser window, sign on tooyour **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="16b11-166">Hello 메뉴에서 hello 위에 표시를 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-166">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="16b11-167">![설정](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "설정")</span><span class="sxs-lookup"><span data-stu-id="16b11-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="16b11-168">페이지 맨 아래에 있는 **계정**</span><span class="sxs-lookup"><span data-stu-id="16b11-168">Click **Account**</span></span>
   
    <span data-ttu-id="16b11-169">![계정](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "계정")</span><span class="sxs-lookup"><span data-stu-id="16b11-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="16b11-170">Hello 클릭 **보안 및 인증** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-170">Click hello **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="16b11-171">![보안 및 인증](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "보안 및 인증")</span><span class="sxs-lookup"><span data-stu-id="16b11-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="16b11-172">Hello에 **설치 프로그램에서 Single Sign-on** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-172">In hello **Setup Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="16b11-173">![Single Sign-On 설정](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="16b11-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="16b11-174">a.</span><span class="sxs-lookup"><span data-stu-id="16b11-174">a.</span></span> <span data-ttu-id="16b11-175">**Single Sign-On 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="16b11-176">b.</span><span class="sxs-lookup"><span data-stu-id="16b11-176">b.</span></span> <span data-ttu-id="16b11-177">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **Login Page URL**(로그인 페이지 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="16b11-178">c.</span><span class="sxs-lookup"><span data-stu-id="16b11-178">c.</span></span> <span data-ttu-id="16b11-179">Azure Portal에서 복사한 **로그아웃 URL**을 **Logout Page URL**(로그아웃 페이지 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="16b11-180">d.</span><span class="sxs-lookup"><span data-stu-id="16b11-180">d.</span></span> <span data-ttu-id="16b11-181">Azure Portal에서 복사한 **SAML 엔터티 ID**를 **ID 공급자 발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="16b11-182">e.</span><span class="sxs-lookup"><span data-stu-id="16b11-182">e.</span></span> <span data-ttu-id="16b11-183">**확인 인증서**, 클릭 **파일 선택**, 한 다음 Azure 포털에서 다운로드 한 hello 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-183">In **Verification Certificate**, click **Choose file**, and then upload hello certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="16b11-184">f.</span><span class="sxs-lookup"><span data-stu-id="16b11-184">f.</span></span> <span data-ttu-id="16b11-185">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="16b11-186">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="16b11-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="16b11-187">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="16b11-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="16b11-188">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="16b11-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="16b11-189">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="16b11-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="16b11-190">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="16b11-192">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="16b11-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="16b11-193">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="16b11-195">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="16b11-197">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="16b11-199">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="16b11-201">a.</span><span class="sxs-lookup"><span data-stu-id="16b11-201">a.</span></span> <span data-ttu-id="16b11-202">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16b11-203">b.</span><span class="sxs-lookup"><span data-stu-id="16b11-203">b.</span></span> <span data-ttu-id="16b11-204">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="16b11-205">c.</span><span class="sxs-lookup"><span data-stu-id="16b11-205">c.</span></span> <span data-ttu-id="16b11-206">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="16b11-207">d.</span><span class="sxs-lookup"><span data-stu-id="16b11-207">d.</span></span> <span data-ttu-id="16b11-208">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="16b11-209">ThousandEyes 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="16b11-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="16b11-210">Tooenable Azure AD 사용자가 toolog ThousandEyes에 주문 하 고에 ThousandEyes에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-210">In order tooenable Azure AD users toolog into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="16b11-211">Hello ThousandEyes의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-211">In hello case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="16b11-212">다른 ThousandEyes 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 사용자 계정을 ThousandEyes tooprovision Azure Active Directory에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="16b11-213">**사용자 계정 tooThousandEyes tooprovision hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="16b11-213">**tooprovision a user account tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="16b11-214">ThousandEyes 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="16b11-215">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="16b11-216">![설정](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "설정")</span><span class="sxs-lookup"><span data-stu-id="16b11-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="16b11-217">**계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-217">Click **Account**.</span></span>
   
    <span data-ttu-id="16b11-218">![계정](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "계정")</span><span class="sxs-lookup"><span data-stu-id="16b11-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="16b11-219">Hello 클릭 **계정 및 사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-219">Click hello **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="16b11-220">![계정 및 사용자](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "계정 및 사용자")</span><span class="sxs-lookup"><span data-stu-id="16b11-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="16b11-221">Hello에 **사용자 추가 및 계정** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-221">In hello **Add Users & Accounts** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="16b11-222">![사용자 계정 추가](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "사용자 계정 추가")</span><span class="sxs-lookup"><span data-stu-id="16b11-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="16b11-223">a.</span><span class="sxs-lookup"><span data-stu-id="16b11-223">a.</span></span> <span data-ttu-id="16b11-224">**이름** 텍스트 상자와 같은 사용자의 형식 hello 이름 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-224">In **Name** textbox, type hello name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="16b11-225">b.</span><span class="sxs-lookup"><span data-stu-id="16b11-225">b.</span></span> <span data-ttu-id="16b11-226">**전자 메일** 텍스트 형식 hello 전자 메일 사용자의 같은  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-226">In **Email** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="16b11-227">b.</span><span class="sxs-lookup"><span data-stu-id="16b11-227">b.</span></span> <span data-ttu-id="16b11-228">클릭 **새 사용자 추가 tooAccount**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-228">Click **Add New User tooAccount**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="16b11-229">hello Azure Active Directory 계정 소유자 메일 링크 tooconfirm 포함 되며 hello 계정을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-229">hello Azure Active Directory account holder will get an email including a link tooconfirm and activate hello account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="16b11-230">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="16b11-231">이 섹션에서는 tooThousandEyes 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThousandEyes.</span></span>

![사용자 할당][200] 

<span data-ttu-id="16b11-233">**tooassign Britta Simon tooThousandEyes hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="16b11-233">**tooassign Britta Simon tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="16b11-234">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="16b11-236">Hello 응용 프로그램 목록에서 선택 **ThousandEyes**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-236">In hello applications list, select **ThousandEyes**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="16b11-238">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="16b11-240">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-240">Click **Add** button.</span></span> <span data-ttu-id="16b11-241">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="16b11-243">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="16b11-244">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16b11-245">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="16b11-246">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="16b11-246">Testing single sign-on</span></span>

<span data-ttu-id="16b11-247">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="16b11-248">Hello ThousandEyes hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour ThousandEyes 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-248">When you click hello ThousandEyes tile in hello Access Panel, you should get automatically signed-on tooyour ThousandEyes application.</span></span>

<span data-ttu-id="16b11-249">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="16b11-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="16b11-250">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="16b11-250">Additional resources</span></span>

* [<span data-ttu-id="16b11-251">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="16b11-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16b11-252">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="16b11-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png


---
title: "자습서: New Relic과 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 New Relic 간에 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="2d88d-103">자습서: New Relic과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2d88d-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="2d88d-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 New Relic 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-104">In this tutorial, you learn how toointegrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d88d-105">Azure AD와 New Relic 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-105">Integrating New Relic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2d88d-106">액세스 tooNew Relic 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-106">You can control in Azure AD who has access tooNew Relic</span></span>
- <span data-ttu-id="2d88d-107">프로그램 사용자 tooautomatically get 로그온 tooNew Relic (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-107">You can enable your users tooautomatically get signed-on tooNew Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d88d-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2d88d-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d88d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2d88d-110">Prerequisites</span></span>

<span data-ttu-id="2d88d-111">New Relic와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-111">tooconfigure Azure AD integration with New Relic, you need hello following items:</span></span>

- <span data-ttu-id="2d88d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2d88d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d88d-113">New Relic Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2d88d-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d88d-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d88d-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d88d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2d88d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d88d-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d88d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2d88d-118">Scenario description</span></span>
<span data-ttu-id="2d88d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d88d-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d88d-121">Hello 갤러리에서 New Relic 추가</span><span class="sxs-lookup"><span data-stu-id="2d88d-121">Adding New Relic from hello gallery</span></span>
2. <span data-ttu-id="2d88d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2d88d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-hello-gallery"></a><span data-ttu-id="2d88d-123">Hello 갤러리에서 New Relic 추가</span><span class="sxs-lookup"><span data-stu-id="2d88d-123">Adding New Relic from hello gallery</span></span>
<span data-ttu-id="2d88d-124">tooconfigure hello와의 통합 New Relic Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 New Relic tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-124">tooconfigure hello integration of New Relic into Azure AD, you need tooadd New Relic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2d88d-125">**hello 갤러리에서 New Relic tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d88d-125">**tooadd New Relic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d88d-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2d88d-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2d88d-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="2d88d-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="2d88d-133">Hello 검색 상자에 입력 **New Relic**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-133">In hello search box, type **New Relic**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="2d88d-135">Hello 결과 패널에서 선택 **New Relic**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-135">In hello results panel, select **New Relic**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d88d-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2d88d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2d88d-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 New Relic에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2d88d-139">Single sign on toowork에 대 한 Azure AD는 tooknow New Relic에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in New Relic is tooa user in Azure AD.</span></span> <span data-ttu-id="2d88d-140">즉, Azure AD 사용자와 New Relic에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-140">In other words, a link relationship between an Azure AD user and hello related user in New Relic needs toobe established.</span></span>

<span data-ttu-id="2d88d-141">New Relic에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-141">In New Relic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2d88d-142">tooconfigure와 New Relic를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-142">tooconfigure and test Azure AD single sign-on with New Relic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2d88d-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2d88d-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d88d-145">**[New Relic 테스트 사용자 만들기](#creating-a-new-relic-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 New Relic에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - toohave a counterpart of Britta Simon in New Relic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2d88d-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d88d-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="2d88d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d88d-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2d88d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d88d-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 New Relic 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="2d88d-150">**Azure AD tooconfigure single sign on와 New Relic hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d88d-150">**tooconfigure Azure AD single sign-on with New Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d88d-151">Hello hello에 Azure 포털에서에서 **New Relic** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-151">In hello Azure portal, on hello **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="2d88d-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="2d88d-155">Hello에 **새 Relic 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-155">On hello **New Relic Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="2d88d-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="2d88d-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2d88d-158">hello 값이 실제 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-158">hello value is not real.</span></span> <span data-ttu-id="2d88d-159">업데이트 hello 값과 실제 로그온 URL hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="2d88d-160">연락처 [새 Relic 클라이언트 지원 팀](https://support.newrelic.com/) tooget hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-160">Contact [New Relic Client support team](https://support.newrelic.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="2d88d-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="2d88d-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2d88d-165">Hello에 **새 Relic 구성** 섹션에서 클릭 **New Relic 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="2d88d-165">On hello **New Relic Configuration** section, click **Configure New Relic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2d88d-166">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="2d88d-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="2d88d-168">다른 웹 브라우저 창에서 tooyour 로그인 **New Relic** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-168">In a different web browser window, sign on tooyour **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="2d88d-169">Hello 메뉴에서 hello 위에 표시를 클릭 **계정 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-169">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="2d88d-170">![계정 설정](./media/active-directory-saas-new-relic-tutorial/ic797036.png "계정 설정")</span><span class="sxs-lookup"><span data-stu-id="2d88d-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="2d88d-171">Hello 클릭 **보안 및 인증** 탭을 클릭 한 다음 hello **Single sign on** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-171">Click hello **Security and authentication** tab, and then click hello **Single sign on** tab.</span></span>
   
    <span data-ttu-id="2d88d-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2d88d-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="2d88d-173">Hello SAML 대화 상자 페이지에서 다음 단계는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-173">On hello SAML dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="2d88d-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="2d88d-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="2d88d-175">a.</span><span class="sxs-lookup"><span data-stu-id="2d88d-175">a.</span></span> <span data-ttu-id="2d88d-176">클릭 **파일 선택** tooupload 다운로드 한 Azure Active Directory 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-176">Click **Choose File** tooupload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="2d88d-177">b.</span><span class="sxs-lookup"><span data-stu-id="2d88d-177">b.</span></span> <span data-ttu-id="2d88d-178">Hello에 **원격 로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-178">In hello **Remote login URL** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="2d88d-179">c.</span><span class="sxs-lookup"><span data-stu-id="2d88d-179">c.</span></span> <span data-ttu-id="2d88d-180">Hello에 **로그 아웃 방문 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-180">In hello **Logout landing URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="2d88d-181">d.</span><span class="sxs-lookup"><span data-stu-id="2d88d-181">d.</span></span> <span data-ttu-id="2d88d-182">**내 변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="2d88d-183">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="2d88d-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2d88d-184">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="2d88d-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2d88d-185">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2d88d-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d88d-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2d88d-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d88d-187">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="2d88d-189">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d88d-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d88d-190">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d88d-192">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d88d-194">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d88d-196">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d88d-198">a.</span><span class="sxs-lookup"><span data-stu-id="2d88d-198">a.</span></span> <span data-ttu-id="2d88d-199">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d88d-200">b.</span><span class="sxs-lookup"><span data-stu-id="2d88d-200">b.</span></span> <span data-ttu-id="2d88d-201">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d88d-202">c.</span><span class="sxs-lookup"><span data-stu-id="2d88d-202">c.</span></span> <span data-ttu-id="2d88d-203">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2d88d-204">d.</span><span class="sxs-lookup"><span data-stu-id="2d88d-204">d.</span></span> <span data-ttu-id="2d88d-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="2d88d-206">New Relic 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2d88d-206">Creating a New Relic test user</span></span>

<span data-ttu-id="2d88d-207">Tooenable Azure Active Directory 사용자 toolog tooNew Relic에에서 주문 하 고에서 New Relic에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-207">In order tooenable Azure Active Directory users toolog in tooNew Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="2d88d-208">Hello New Relic의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-208">In hello case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="2d88d-209">**사용자 계정 tooNew Relic tooprovision hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d88d-209">**tooprovision a user account tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d88d-210">Tooyour 로그인 **New Relic** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-210">Log in tooyour **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="2d88d-211">Hello 메뉴에서 hello 위에 표시를 클릭 **계정 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-211">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="2d88d-212">![계정 설정](./media/active-directory-saas-new-relic-tutorial/ic797040.png "계정 설정")</span><span class="sxs-lookup"><span data-stu-id="2d88d-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="2d88d-213">Hello에 **계정** hello 창 왼쪽을 클릭 **요약**, 클릭 하 고 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-213">In hello **Account** pane on hello left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="2d88d-214">![계정 설정](./media/active-directory-saas-new-relic-tutorial/ic797041.png "계정 설정")</span><span class="sxs-lookup"><span data-stu-id="2d88d-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="2d88d-215">Hello에 **활성 사용자** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-215">On hello **Active users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="2d88d-216">![활성 사용자](./media/active-directory-saas-new-relic-tutorial/ic797042.png "활성 사용자")</span><span class="sxs-lookup"><span data-stu-id="2d88d-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="2d88d-217">a.</span><span class="sxs-lookup"><span data-stu-id="2d88d-217">a.</span></span> <span data-ttu-id="2d88d-218">Hello에 **전자 메일** 텍스트 형식 hello 전자 메일 주소 하려는 유효한 Azure Active Directory 사용자의 tooprovision 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-218">In hello **Email** textbox, type hello email address of a valid Azure Active Directory user you want tooprovision.</span></span>

    <span data-ttu-id="2d88d-219">b.</span><span class="sxs-lookup"><span data-stu-id="2d88d-219">b.</span></span> <span data-ttu-id="2d88d-220">**역할**로 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="2d88d-221">c.</span><span class="sxs-lookup"><span data-stu-id="2d88d-221">c.</span></span> <span data-ttu-id="2d88d-222">**이 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="2d88d-223">다른 New Relic 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision New Relic에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-223">You can use any other New Relic user account creation tools or APIs provided by New Relic tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2d88d-224">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2d88d-225">이 섹션에서는 액세스 tooNew Relic 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNew Relic.</span></span>

![사용자 할당][200] 

<span data-ttu-id="2d88d-227">**tooassign Britta Simon tooNew Relic hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2d88d-227">**tooassign Britta Simon tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d88d-228">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2d88d-230">Hello 응용 프로그램 목록에서 선택 **New Relic**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-230">In hello applications list, select **New Relic**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="2d88d-232">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="2d88d-234">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-234">Click **Add** button.</span></span> <span data-ttu-id="2d88d-235">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="2d88d-237">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2d88d-238">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d88d-239">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2d88d-240">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2d88d-240">Testing single sign-on</span></span>

<span data-ttu-id="2d88d-241">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-241">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2d88d-242">Hello 액세스 패널에서에서 hello New Relic 타일을 클릭할 때 자동으로 로그온 tooyour New Relic 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d88d-242">When you click hello New Relic tile in hello Access Panel, you should get automatically signed-on tooyour New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2d88d-243">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2d88d-243">Additional resources</span></span>

* [<span data-ttu-id="2d88d-244">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="2d88d-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d88d-245">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2d88d-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png


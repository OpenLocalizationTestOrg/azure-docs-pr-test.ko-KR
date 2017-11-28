---
title: "자습서: Bime와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Bime 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1213725028dd8ce90f22fa6e9c50ffabebc8f3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="f01c9-103">자습서: Bime와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f01c9-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="f01c9-104">이 자습서에 설명 어떻게 toointegrate Bime와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f01c9-104">In this tutorial, you learn how toointegrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f01c9-105">Azure AD와 Bime 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-105">Integrating Bime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f01c9-106">액세스 tooBime을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-106">You can control in Azure AD who has access tooBime</span></span>
- <span data-ttu-id="f01c9-107">프로그램 사용자 tooautomatically get 로그온 tooBime (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-107">You can enable your users tooautomatically get signed-on tooBime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f01c9-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f01c9-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f01c9-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f01c9-110">Prerequisites</span></span>

<span data-ttu-id="f01c9-111">Bime와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-111">tooconfigure Azure AD integration with Bime, you need hello following items:</span></span>

- <span data-ttu-id="f01c9-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f01c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f01c9-113">Bime Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f01c9-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f01c9-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f01c9-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f01c9-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f01c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f01c9-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f01c9-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f01c9-118">Scenario description</span></span>
<span data-ttu-id="f01c9-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f01c9-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f01c9-121">Bime는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="f01c9-121">Adding Bime from hello gallery</span></span>
2. <span data-ttu-id="f01c9-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f01c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-hello-gallery"></a><span data-ttu-id="f01c9-123">Bime는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="f01c9-123">Adding Bime from hello gallery</span></span>
<span data-ttu-id="f01c9-124">tooconfigure hello와의 통합 Bime Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Bime tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-124">tooconfigure hello integration of Bime into Azure AD, you need tooadd Bime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f01c9-125">**Bime hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f01c9-125">**tooadd Bime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f01c9-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f01c9-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f01c9-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="f01c9-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="f01c9-133">Hello 검색 상자에 입력 **Bime**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-133">In hello search box, type **Bime**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="f01c9-135">Hello 결과 패널에서 선택 **Bime**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-135">In hello results panel, select **Bime**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f01c9-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f01c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f01c9-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Bime에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f01c9-139">Single sign on toowork에 대 한 Azure AD는 tooknow Bime에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bime is tooa user in Azure AD.</span></span> <span data-ttu-id="f01c9-140">즉, Azure AD 사용자와 Bime에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-140">In other words, a link relationship between an Azure AD user and hello related user in Bime needs toobe established.</span></span>

<span data-ttu-id="f01c9-141">Bime에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-141">In Bime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f01c9-142">tooconfigure와 Bime와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-142">tooconfigure and test Azure AD single sign-on with Bime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f01c9-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f01c9-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f01c9-145">**[Bime 테스트 사용자 만들기](#creating-a-bime-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Bime에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - toohave a counterpart of Britta Simon in Bime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f01c9-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f01c9-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="f01c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f01c9-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f01c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f01c9-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Bime 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="f01c9-150">**Azure AD tooconfigure single sign on와 Bime를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f01c9-150">**tooconfigure Azure AD single sign-on with Bime, perform hello following steps:**</span></span>

1. <span data-ttu-id="f01c9-151">Hello hello에 Azure 포털에서에서 **Bime** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-151">In hello Azure portal, on hello **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="f01c9-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="f01c9-155">Hello에 **Bime 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-155">On hello **Bime Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="f01c9-157">a.</span><span class="sxs-lookup"><span data-stu-id="f01c9-157">a.</span></span> <span data-ttu-id="f01c9-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="f01c9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="f01c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="f01c9-159">b.</span></span> <span data-ttu-id="f01c9-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="f01c9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f01c9-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-161">These values are not real.</span></span> <span data-ttu-id="f01c9-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f01c9-163">연락처 [Bime 클라이언트 지원 팀](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget these values.</span></span> 
 
4. <span data-ttu-id="f01c9-164">Hello에 **SAML 서명 인증서** 섹션을 복사 hello **지문** hello 인증서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="f01c9-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f01c9-168">Hello에 **Bime 구성** 섹션에서 클릭 **구성 Bime** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="f01c9-168">On hello **Bime Configuration** section, click **Configure Bime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f01c9-169">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="f01c9-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="f01c9-171">다른 웹 브라우저 창에서 Bime 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="f01c9-172">Hello 도구 모음에서 클릭 **Admin**, 차례로 **계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-172">In hello toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="f01c9-173">![관리자](./media/active-directory-saas-bime-tutorial/ic775558.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="f01c9-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="f01c9-174">Hello 계정 구성 페이지에서 다음 단계는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-174">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="f01c9-175">![Single Sign-On 구성](./media/active-directory-saas-bime-tutorial/ic775559.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="f01c9-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="f01c9-176">a.</span><span class="sxs-lookup"><span data-stu-id="f01c9-176">a.</span></span> <span data-ttu-id="f01c9-177">**SAML 인증 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="f01c9-178">b.</span><span class="sxs-lookup"><span data-stu-id="f01c9-178">b.</span></span> <span data-ttu-id="f01c9-179">Hello에 **원격 로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-179">In hello **Remote Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f01c9-180">c.</span><span class="sxs-lookup"><span data-stu-id="f01c9-180">c.</span></span>  <span data-ttu-id="f01c9-181">붙여넣기 hello **지문** hello에 Azure 포털에서 값 **인증서 지문** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-181">Paste hello **Thumbprint** value from Azure portal into hello **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="f01c9-182">d.</span><span class="sxs-lookup"><span data-stu-id="f01c9-182">d.</span></span> <span data-ttu-id="f01c9-183">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f01c9-184">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="f01c9-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f01c9-185">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="f01c9-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f01c9-186">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f01c9-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f01c9-187">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f01c9-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="f01c9-188">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="f01c9-190">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f01c9-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f01c9-191">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f01c9-193">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f01c9-195">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f01c9-197">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f01c9-199">a.</span><span class="sxs-lookup"><span data-stu-id="f01c9-199">a.</span></span> <span data-ttu-id="f01c9-200">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f01c9-201">b.</span><span class="sxs-lookup"><span data-stu-id="f01c9-201">b.</span></span> <span data-ttu-id="f01c9-202">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f01c9-203">c.</span><span class="sxs-lookup"><span data-stu-id="f01c9-203">c.</span></span> <span data-ttu-id="f01c9-204">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f01c9-205">d.</span><span class="sxs-lookup"><span data-stu-id="f01c9-205">d.</span></span> <span data-ttu-id="f01c9-206">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="f01c9-207">Bime 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f01c9-207">Creating a Bime test user</span></span>

<span data-ttu-id="f01c9-208">Tooenable Azure AD 사용자가 toolog tooBime에 주문 하 고에 Bime에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-208">In order tooenable Azure AD users toolog in tooBime, they must be provisioned into Bime.</span></span> <span data-ttu-id="f01c9-209">Hello Bime의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-209">In hello case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="f01c9-210">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="f01c9-210">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="f01c9-211">Tooyour 로그인 **Bime** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-211">Log in tooyour **Bime** tenant.</span></span>

2. <span data-ttu-id="f01c9-212">Hello 도구 모음에서 클릭 **Admin**, 차례로 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-212">In hello toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="f01c9-213">![관리자](./media/active-directory-saas-bime-tutorial/ic775561.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="f01c9-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="f01c9-214">Hello에 **사용자 목록**, 클릭 **새 사용자 추가** ("+").</span><span class="sxs-lookup"><span data-stu-id="f01c9-214">In hello **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="f01c9-215">![사용자](./media/active-directory-saas-bime-tutorial/ic775562.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="f01c9-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="f01c9-216">Hello에 **사용자 세부 정보** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-216">On hello **User Details** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="f01c9-217">![사용자 세부 정보](./media/active-directory-saas-bime-tutorial/ic775563.png "사용자 세부 정보")</span><span class="sxs-lookup"><span data-stu-id="f01c9-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="f01c9-218">a.</span><span class="sxs-lookup"><span data-stu-id="f01c9-218">a.</span></span> <span data-ttu-id="f01c9-219">Hello에 **이름** textbox hello와 같은 사용자의 이름을 입력 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-219">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="f01c9-220">b.</span><span class="sxs-lookup"><span data-stu-id="f01c9-220">b.</span></span> <span data-ttu-id="f01c9-221">Hello에 **성** textbox hello와 같은 사용자의 성을 입력 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-221">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="f01c9-222">c.</span><span class="sxs-lookup"><span data-stu-id="f01c9-222">c.</span></span> <span data-ttu-id="f01c9-223">Hello에 **전자 메일** 텍스트 상자와 같은 사용자의 전자 메일을 hello 입력  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-223">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="f01c9-224">d.</span><span class="sxs-lookup"><span data-stu-id="f01c9-224">d.</span></span> <span data-ttu-id="f01c9-225">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="f01c9-226">다른 Bime 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Bime에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-226">You can use any other Bime user account creation tools or APIs provided by Bime tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f01c9-227">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f01c9-228">이 섹션에서는 tooBime 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBime.</span></span>

![사용자 할당][200] 

<span data-ttu-id="f01c9-230">**tooassign Britta Simon tooBime hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f01c9-230">**tooassign Britta Simon tooBime, perform hello following steps:**</span></span>

1. <span data-ttu-id="f01c9-231">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f01c9-233">Hello 응용 프로그램 목록에서 선택 **Bime**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-233">In hello applications list, select **Bime**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="f01c9-235">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="f01c9-237">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-237">Click **Add** button.</span></span> <span data-ttu-id="f01c9-238">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="f01c9-240">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f01c9-241">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f01c9-242">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f01c9-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f01c9-243">Testing single sign-on</span></span>

<span data-ttu-id="f01c9-244">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-244">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f01c9-245">Hello 액세스 패널에서에서 hello Bime 타일을 클릭할 때 자동으로 로그온 tooyour Bime 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f01c9-245">When you click hello Bime tile in hello Access Panel, you should get automatically signed-on tooyour Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f01c9-246">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f01c9-246">Additional resources</span></span>

* [<span data-ttu-id="f01c9-247">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="f01c9-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f01c9-248">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f01c9-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png


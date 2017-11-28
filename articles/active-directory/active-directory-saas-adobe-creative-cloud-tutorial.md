---
title: "자습서: Adobe Creative Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Adobe 크리에이티브 클라우드 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="5abda-103">자습서: Adobe Creative Cloud와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5abda-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="5abda-104">배웁니다이 자습서에서는 Azure Active Directory (Azure AD)와 toointegrate Adobe 크리에이티브 클라우드 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-104">In this tutorial, you learn how toointegrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5abda-105">Azure AD와 Adobe 크리에이티브 클라우드 통합 이점을 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="5abda-105">Integrating Adobe Creative Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5abda-106">크리에이티브 클라우드 액세스 tooAdobe을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-106">You can control in Azure AD who has access tooAdobe Creative Cloud</span></span>
- <span data-ttu-id="5abda-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooAdobe 크리에이티브 클라우드 (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-107">You can enable your users tooautomatically get signed-on tooAdobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5abda-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="5abda-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5abda-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5abda-110">Prerequisites</span></span>

<span data-ttu-id="5abda-111">Adobe 크리에이티브 클라우드와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-111">tooconfigure Azure AD integration with Adobe Creative Cloud, you need hello following items:</span></span>

- <span data-ttu-id="5abda-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5abda-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5abda-113">Adobe Creative Cloud Single Sign-On을 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5abda-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5abda-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5abda-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5abda-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5abda-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5abda-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5abda-118">Scenario description</span></span>
<span data-ttu-id="5abda-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5abda-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5abda-121">Hello 갤러리에서 Adobe 크리에이티브 클라우드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-121">Adding Adobe Creative Cloud from hello gallery</span></span>
2. <span data-ttu-id="5abda-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5abda-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a><span data-ttu-id="5abda-123">Hello 갤러리에서 Adobe 크리에이티브 클라우드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-123">Adding Adobe Creative Cloud from hello gallery</span></span>
<span data-ttu-id="5abda-124">tooconfigure hello와의 통합 Adobe 크리에이티브 클라우드 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Adobe 크리에이티브 클라우드 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-124">tooconfigure hello integration of Adobe Creative Cloud into Azure AD, you need tooadd Adobe Creative Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5abda-125">**hello 갤러리에서 Adobe 크리에이티브 클라우드 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5abda-125">**tooadd Adobe Creative Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5abda-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5abda-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5abda-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5abda-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5abda-133">Hello 검색 상자에 입력 **Adobe 크리에이티브 클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-133">In hello search box, type **Adobe Creative Cloud**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="5abda-135">Hello 결과 패널에서 선택 **Adobe 크리에이티브 클라우드**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-135">In hello results panel, select **Adobe Creative Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5abda-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5abda-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5abda-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Adobe Creative Cloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5abda-139">Single sign on toowork에 대 한 Azure AD는 tooknow Adobe 크리에이티브 클라우드에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Creative Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="5abda-140">즉, Azure AD 사용자 및 Adobe 크리에이티브 클라우드에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Creative Cloud needs toobe established.</span></span>

<span data-ttu-id="5abda-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Adobe 크리에이티브 클라우드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="5abda-142">tooconfigure 및 Adobe 크리에이티브 클라우드를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-142">tooconfigure and test Azure AD single sign-on with Adobe Creative Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5abda-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5abda-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5abda-145">**[Adobe 크리에이티브 클라우드 테스트 사용자 만들기](#creating-an-adobe-creative-cloud-test-user)**  -toohave Britta Simon 표현인 연결 된 Azure AD toohello 그녀는 Adobe 크리에이티브 클라우드에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - toohave a counterpart of Britta Simon in Adobe Creative Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="5abda-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5abda-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="5abda-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5abda-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5abda-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5abda-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 Adobe 크리에이티브 클라우드 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="5abda-150">**Adobe 크리에이티브 클라우드와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5abda-150">**tooconfigure Azure AD single sign-on with Adobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="5abda-151">Hello에 hello Azure 관리 포털에서 **Adobe 크리에이티브 클라우드** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-151">In hello Azure Management portal, on hello **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5abda-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="5abda-155">Hello에 **Adobe 창조적인 클라우드 도메인 및 Url** 섹션를 hello tooconfigure hello 응용 프로그램에 필요한 경우 다음 단계를 수행 **IDP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="5abda-155">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="5abda-157">a.</span><span class="sxs-lookup"><span data-stu-id="5abda-157">a.</span></span> <span data-ttu-id="5abda-158">Hello에 **식별자** 형식 hello 값으로 텍스트 상자:`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="5abda-158">In hello **Identifier** textbox, type hello value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="5abda-159">b.</span><span class="sxs-lookup"><span data-stu-id="5abda-159">b.</span></span> <span data-ttu-id="5abda-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="5abda-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5abda-161">이러한 없는지 hello 실제 값 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5abda-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="5abda-162">Tooupdate hello 실제 식별자와 회신 URL 사용 하 여 이러한 값 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="5abda-163">여기 있습니다 toouse hello의 고유 값을 hello 식별자의에서 문자열을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="5abda-164">Toocreate 된 사용자를 수동으로 해야 할 경우 toocontact hello Adobe 크리에이티브 클라우드 지원 팀을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-164">If you need toocreate an user manually, you need toocontact hello Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="5abda-165">Hello에 **Adobe 창조적인 클라우드 도메인 및 Url** 섹션를 hello tooconfigure hello 응용 프로그램에 필요한 경우 다음 단계를 수행 **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="5abda-165">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="5abda-167">a.</span><span class="sxs-lookup"><span data-stu-id="5abda-167">a.</span></span> <span data-ttu-id="5abda-168">Hello 클릭 **고급 URL 설정 표시** 옵션</span><span class="sxs-lookup"><span data-stu-id="5abda-168">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="5abda-169">b.</span><span class="sxs-lookup"><span data-stu-id="5abda-169">b.</span></span> <span data-ttu-id="5abda-170">Hello에 **로그온 URL** 형식 hello 값으로 텍스트 상자:`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="5abda-170">In hello **Sign-on URL** textbox, type hello value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="5abda-171">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-171">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="5abda-173">Hello에 **Adobe 창조적인 클라우드 구성** 섹션에서 클릭 **Adobe 크리에이티브 클라우드 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="5abda-173">On hello **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5abda-174">Hello를 복사 하십시오 **SAML 엔터티 Id** 및 **SAML SSO 서비스 URL** 빠른 참조 섹션에서.</span><span class="sxs-lookup"><span data-stu-id="5abda-174">Please copy hello **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="5abda-176">다른 웹 브라우저 창에서 관리자 권한으로 로그온 tooyour Adobe 크리에이티브 클라우드 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-176">In a different web browser window, sign-on tooyour Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="5abda-177">너무 이동**Identity** 왼쪽된 탐색 창의 hello 되 고 도메인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-177">Go too**Identity** on hello left navigation pane and click your domain.</span></span> <span data-ttu-id="5abda-178">다음에 나오는 단계에 따라 hello 수행 **Single Sign 구성이 필요** 섹션.</span><span class="sxs-lookup"><span data-stu-id="5abda-178">Then perform hello following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="5abda-179">![설정](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "설정")</span><span class="sxs-lookup"><span data-stu-id="5abda-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="5abda-180">클릭 **찾아보기** tooupload hello Azure AD에서 너무 인증서를 다운로드**IDP 인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-180">Click **Browse** tooupload hello downloaded certificate from Azure AD too**IDP Certificate**.</span></span>

10. <span data-ttu-id="5abda-181">Hello에 **IDP 발급자** hello 값의 텍스트 상자 **SAML 엔터티 Id** 에서 복사할 **sign on 구성** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="5abda-181">In hello **IDP issuer** textbox, put hello value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="5abda-182">Hello에 **IDP 로그인 URL** hello 값의 텍스트 상자 **SAML SSO 서비스 URL** 에서 복사할 **sign on 구성** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="5abda-182">In hello **IDP Login URL** textbox, put hello value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="5abda-183">**HTTP - 리디렉션**을 **IDP 바인딩**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="5abda-184">**전자 메일 주소**를 **사용자 로그인 설정**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="5abda-185">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-185">Click **Save** button.</span></span>

15. <span data-ttu-id="5abda-186">hello XML hello 대시보드를 제공 합니다 **"메타 데이터 다운로드"** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-186">hello dashboard will now present hello XML **"Download Metadata"** file.</span></span> <span data-ttu-id="5abda-187">여기에는 Adobe의 EntityDescriptor URL과 AssertionConsumerService URL이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="5abda-188">Hello 파일을 열고 hello Azure AD 응용 프로그램에서에서 해당 설정을 구성 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5abda-188">Please open hello file and configure them in hello Azure AD application.</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="5abda-191">a.</span><span class="sxs-lookup"><span data-stu-id="5abda-191">a.</span></span> <span data-ttu-id="5abda-192">사용 하 여 hello Adobe EntityDescriptor 값에 대 한 정보가 제공 **식별자** hello에 **앱 설정 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="5abda-192">Use hello EntityDescriptor value Adobe provided you for **Identifier** on hello **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="5abda-193">b.</span><span class="sxs-lookup"><span data-stu-id="5abda-193">b.</span></span> <span data-ttu-id="5abda-194">사용 하 여 hello Adobe AssertionConsumerService 값에 대 한 정보가 제공 **회신 URL** hello에 **앱 설정 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="5abda-194">Use hello AssertionConsumerService value Adobe provided you for **Reply URL** on hello **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5abda-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5abda-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="5abda-196">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-196">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5abda-198">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5abda-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5abda-199">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-199">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5abda-201">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-201">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5abda-203">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="5abda-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5abda-205">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5abda-207">a.</span><span class="sxs-lookup"><span data-stu-id="5abda-207">a.</span></span> <span data-ttu-id="5abda-208">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5abda-209">b.</span><span class="sxs-lookup"><span data-stu-id="5abda-209">b.</span></span> <span data-ttu-id="5abda-210">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5abda-211">c.</span><span class="sxs-lookup"><span data-stu-id="5abda-211">c.</span></span> <span data-ttu-id="5abda-212">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5abda-213">d.</span><span class="sxs-lookup"><span data-stu-id="5abda-213">d.</span></span> <span data-ttu-id="5abda-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="5abda-215">Adobe Creative Cloud 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5abda-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="5abda-216">Tooenable Azure AD 사용자가 toolog Adobe 크리에이티브 클라우드로 주문 하 고에 Adobe 크리에이티브 클라우드에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-216">In order tooenable Azure AD users toolog into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="5abda-217">Hello Adobe 크리에이티브 클라우드의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-217">In hello case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="5abda-218">**사용자 계정 수행 tooprovision hello 다음 단계:**</span><span class="sxs-lookup"><span data-stu-id="5abda-218">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="5abda-219">관리자 권한으로 Adobe 크리에이티브 클라우드 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-219">Log in tooyour Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="5abda-220">**피플**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-220">Click **People**.</span></span>

    <span data-ttu-id="5abda-221">![사람](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "사람")</span><span class="sxs-lookup"><span data-stu-id="5abda-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="5abda-222">**사용자 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-222">Click **Invite User**.</span></span>

    <span data-ttu-id="5abda-223">![사용자 초대](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "사용자 초대")</span><span class="sxs-lookup"><span data-stu-id="5abda-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="5abda-224">Hello에 **사용자 초대** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-224">On hello **Invite People** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="5abda-225">![피플 초대](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "피플 초대")</span><span class="sxs-lookup"><span data-stu-id="5abda-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="5abda-226">a.</span><span class="sxs-lookup"><span data-stu-id="5abda-226">a.</span></span> <span data-ttu-id="5abda-227">Hello에 **전자 메일** textbox Britta Simon 계정의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-227">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="5abda-228">b.</span><span class="sxs-lookup"><span data-stu-id="5abda-228">b.</span></span> <span data-ttu-id="5abda-229">**초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5abda-230">hello Azure Active Directory 계정 소유자 전자 메일을 받게 되 고 링크 tooconfirm 자신의 계정을 활성화 되기 전에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5abda-231">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5abda-232">이 섹션에서는 그녀의 액세스 tooAdobe 크리에이티브 클라우드를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAdobe Creative Cloud.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5abda-234">**tooassign Britta Simon tooAdobe 크리에이티브 클라우드 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5abda-234">**tooassign Britta Simon tooAdobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="5abda-235">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-235">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5abda-237">Hello 응용 프로그램 목록에서 선택 **Adobe 크리에이티브 클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-237">In hello applications list, select **Adobe Creative Cloud**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="5abda-239">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5abda-241">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-241">Click **Add** button.</span></span> <span data-ttu-id="5abda-242">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5abda-244">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5abda-245">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5abda-246">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5abda-247">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5abda-247">Testing single sign-on</span></span>

<span data-ttu-id="5abda-248">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5abda-249">Hello 액세스 패널에서에서 hello Adobe 크리에이티브 클라우드 타일을 클릭할 때 자동으로 로그온 tooyour Adobe 크리에이티브 클라우드 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5abda-249">When you click hello Adobe Creative Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5abda-250">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5abda-250">Additional resources</span></span>

* [<span data-ttu-id="5abda-251">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="5abda-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5abda-252">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5abda-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png
---
title: "자습서: JIRA SAML SSO by Microsoft와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory 및 Microsoft에서 JIRA SAML SSO 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="e01d1-103">자습서: JIRA SAML SSO by Microsoft와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="e01d1-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="e01d1-104">이 자습서에 설명 어떻게 toointegrate JIRA SAML SSO microsoft Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e01d1-104">In this tutorial, you learn how toointegrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e01d1-105">다음 이점을 hello로 제공 JIRA SAML SSO microsoft Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="e01d1-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e01d1-106">Microsoft에서 SAML SSO 액세스 tooJIRA 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-106">You can control in Azure AD who has access tooJIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="e01d1-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooJIRA SAML SSO (Single Sign-on)는 Microsoft에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-107">You can enable your users tooautomatically get signed-on tooJIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e01d1-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e01d1-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e01d1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e01d1-110">Prerequisites</span></span>

<span data-ttu-id="e01d1-111">Microsoft에서 JIRA SAML SSO와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-111">tooconfigure Azure AD integration with JIRA SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="e01d1-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="e01d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e01d1-113">Windows 64 비트 서버 (온-프레미스 또는 클라우드에서 hello IaaS 인프라)에 설치 된 JIRA 서버 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="e01d1-113">JIRA server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="e01d1-114">JIRA 서버에서 HTTPS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="e01d1-115">JIRA 플러그 인에 대 한 참고 hello 지원 버전은 아래 섹션에서 언급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-115">Note hello supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="e01d1-116">JIRA 서버는 인터넷에 연결할 수 있는 인증을 위해 특히 tooAzure AD 로그인 페이지 및 해야 수 tooreceive Azure AD에서 토큰 hello.</span><span class="sxs-lookup"><span data-stu-id="e01d1-116">JIRA server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="e01d1-117">JIRA에 관리자 자격 증명이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="e01d1-118">JIRA에서 WebSudo를 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="e01d1-119">Hello JIRA 서버 응용 프로그램에서에서 만든 사용자를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-119">Test user created in hello JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="e01d1-120">이 자습서의 단계를 tootest hello, 권장 하지는 않습니다 JIRA의 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-120">tootest hello steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="e01d1-121">개발 이나 준비 hello 응용 프로그램의 환경 및 사용 하 여 hello 프로덕션 환경에 먼저 hello 통합을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="e01d1-122">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e01d1-123">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e01d1-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e01d1-124">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="e01d1-125">지원되는 JIRA 버전</span><span class="sxs-lookup"><span data-stu-id="e01d1-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="e01d1-126">현재 기준으로 다음 버전의 JIRA가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="e01d1-127">JIRA 코어 및 소프트웨어: 6.0 too7.2.0</span><span class="sxs-lookup"><span data-stu-id="e01d1-127">JIRA Core and Software: 6.0 too7.2.0</span></span>
- <span data-ttu-id="e01d1-128">3.0 too3.2 JIRA 서비스 데스크:</span><span class="sxs-lookup"><span data-stu-id="e01d1-128">JIRA Service Desk: 3.0 too3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e01d1-129">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="e01d1-129">Scenario description</span></span>
<span data-ttu-id="e01d1-130">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e01d1-131">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-131">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e01d1-132">Microsoft에서 JIRA SAML SSO hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="e01d1-132">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="e01d1-133">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e01d1-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="e01d1-134">Microsoft에서 JIRA SAML SSO hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="e01d1-134">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="e01d1-135">tooconfigure hello와의 통합 JIRA SAML SSO microsoft Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Microsoft에서 JIRA SAML SSO tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-135">tooconfigure hello integration of JIRA SAML SSO by Microsoft into Azure AD, you need tooadd JIRA SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e01d1-136">**hello 갤러리, Microsoft에서 JIRA SAML SSO tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e01d1-136">**tooadd JIRA SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e01d1-137">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-137">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e01d1-139">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-139">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e01d1-140">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-140">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="e01d1-142">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-142">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="e01d1-144">Hello 검색 상자에 입력 **Microsoft에서 JIRA SAML SSO**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-144">In hello search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="e01d1-146">Hello 결과 패널에서 선택 **Microsoft에서 JIRA SAML SSO**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-146">In hello results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e01d1-148">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e01d1-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e01d1-149">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 JIRA SAML SSO by Microsoft에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e01d1-150">Single sign on toowork에 대 한 Azure AD는 tooknow Microsoft에서 JIRA SAML SSO에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-150">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JIRA SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="e01d1-151">즉, Azure AD 사용자와 Microsoft에서 JIRA SAML SSO에서 관련된 사용자 hello 사이의 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-151">In other words, a link relationship between an Azure AD user and hello related user in JIRA SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="e01d1-152">Microsoft에서 JIRA SAML sso에서는 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-152">In JIRA SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e01d1-153">tooconfigure 및 Microsoft에서 JIRA SAML SSO를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-153">tooconfigure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e01d1-154">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e01d1-155">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e01d1-156">**[Microsoft 테스트 사용자가 JIRA SAML SSO 만들기](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave Britta Simon JIRA SAML SSO는 사용자의 연결 된 Azure AD toohello 표현 하는 Microsoft에서 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e01d1-157">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-157">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e01d1-158">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="e01d1-158">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e01d1-159">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="e01d1-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e01d1-160">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Microsoft 응용 프로그램에서 single sign on JIRA SAML SSO에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-160">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="e01d1-161">**microsoft에서 JIRA SAML SSO와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e01d1-161">**tooconfigure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="e01d1-162">Hello hello에 Azure 포털에서에서 **Microsoft에서 JIRA SAML SSO** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-162">In hello Azure portal, on hello **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="e01d1-164">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-164">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="e01d1-166">Hello에 **Microsoft 도메인 및 Url에서 JIRA SAML SSO** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-166">On hello **JIRA SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="e01d1-168">a.</span><span class="sxs-lookup"><span data-stu-id="e01d1-168">a.</span></span> <span data-ttu-id="e01d1-169">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="e01d1-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="e01d1-170">b.</span><span class="sxs-lookup"><span data-stu-id="e01d1-170">b.</span></span> <span data-ttu-id="e01d1-171">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="e01d1-171">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="e01d1-172">c.</span><span class="sxs-lookup"><span data-stu-id="e01d1-172">c.</span></span> <span data-ttu-id="e01d1-173">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="e01d1-173">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e01d1-174">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-174">These values are not real.</span></span> <span data-ttu-id="e01d1-175">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-175">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e01d1-176">명명된 URL인 경우 포트는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="e01d1-177">이러한 값은 hello 자습서의 뒷부분에 설명 된 Jira 플러그 인의 hello 구성 하는 동안 수신 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-177">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="e01d1-178">toogenerate hello **메타 데이터** url hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-178">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="e01d1-179">a.</span><span class="sxs-lookup"><span data-stu-id="e01d1-179">a.</span></span> <span data-ttu-id="e01d1-180">**앱 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-180">Click **App registrations**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="e01d1-182">b.</span><span class="sxs-lookup"><span data-stu-id="e01d1-182">b.</span></span> <span data-ttu-id="e01d1-183">클릭 **끝점** tooopen **끝점** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e01d1-183">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="e01d1-185">c.</span><span class="sxs-lookup"><span data-stu-id="e01d1-185">c.</span></span> <span data-ttu-id="e01d1-186">Hello 복사 단추 toocopy 클릭 **페더레이션 메타 데이터 문서** url 메모장에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-186">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="e01d1-188">d.</span><span class="sxs-lookup"><span data-stu-id="e01d1-188">d.</span></span> <span data-ttu-id="e01d1-189">이제의 toohello 속성 페이지를 이동 **Microsoft에서 JIRA SAML SSO** 및 복사 hello **응용 프로그램 Id** 를 사용 하 여 **복사** 단추를 메모장에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-189">Now go toohello property page of **JIRA SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="e01d1-191">e.</span><span class="sxs-lookup"><span data-stu-id="e01d1-191">e.</span></span> <span data-ttu-id="e01d1-192">Hello 생성 **메타 데이터 URL** hello 패턴을 사용 하 여: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` hello 플러그 인의 hello 구성에 대 한 나중에 사용 중 이므로 메모장에서이 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-192">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="e01d1-193">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-193">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e01d1-195">연락처 [Microsoft](mailto:waadpartners@microsoft.com) hello 다음 hello JIRA 플러그 인에 대 한 정보로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello JIRA plugin.</span></span>
    
    *   <span data-ttu-id="e01d1-196">고객 이름:</span><span class="sxs-lookup"><span data-stu-id="e01d1-196">Customer Name:</span></span>
    *   <span data-ttu-id="e01d1-197">주 도메인 이름:</span><span class="sxs-lookup"><span data-stu-id="e01d1-197">Primary domain name:</span></span>
    *   <span data-ttu-id="e01d1-198">Azure AD Premium: 예/아니요 (플러그 인 사용 가능한 tooall hello 고객 Free, Basic 및 Premium SKU를 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="e01d1-198">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="e01d1-199">이 통합을 사용할 사용자의 수:</span><span class="sxs-lookup"><span data-stu-id="e01d1-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="e01d1-200">JIRA 버전:</span><span class="sxs-lookup"><span data-stu-id="e01d1-200">JIRA Version:</span></span>
    *   <span data-ttu-id="e01d1-201">설명:</span><span class="sxs-lookup"><span data-stu-id="e01d1-201">Comments:</span></span>

7. <span data-ttu-id="e01d1-202">다른 웹 브라우저 창에서 관리자 권한으로 tooyour JIRA 인스턴스에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-202">In a different web browser window, log in tooyour JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="e01d1-203">Hello를 누르고 선 위에 마우스를 가져가면 **추가 기능**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-203">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="e01d1-205">추가 기능 탭 섹션에서 **추가 기능 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="e01d1-207">Microsoft에서 제공 하는 hello 플러그 인을 수동으로 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-207">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="e01d1-208">에 나타나는 hello 플러그 인이 설치 되 면 **사용자 설치** 의 추가 기능 섹션 **관리 추가 기능** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e01d1-208">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="e01d1-209">클릭 **구성** tooconfigure hello 새 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-209">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="e01d1-210">구성 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-210">Perform following steps on configuration page:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="e01d1-212">a.</span><span class="sxs-lookup"><span data-stu-id="e01d1-212">a.</span></span> <span data-ttu-id="e01d1-213">**메타 데이터 URL** hello 붙여 **메타 데이터 URL** hello를 클릭 하 고 Azure AD에서 생성 된 **해결** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-213">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="e01d1-214">Hello IdP 메타 데이터 URL을 읽고 모든 hello 필드 정보를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-214">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="e01d1-215">기본 SAML 사용자 ID 위치는 이름 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="e01d1-216">이 tooan 특성 옵션을 변경할 수 있으며 hello 적절 한 특성 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-216">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="e01d1-217">인증서를 하나만 해결 hello 메타 데이터에 오류가 발생 하지는 않도록 hello 앱에 대해 매핑된 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-217">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="e01d1-218">Hello 메타 데이터 확인 시 여러 인증서가 있는 경우 관리자는 오류를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-218">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="e01d1-219">b.</span><span class="sxs-lookup"><span data-stu-id="e01d1-219">b.</span></span> <span data-ttu-id="e01d1-220">복사 hello **식별자, 회신 URL 및 로그온 URL** 값을 붙여 넣을에 **식별자, 회신 URL 및 로그온 URL** 텍스트 상자에 각각 **Microsoft 도메인 및 UrlJIRASAMLSSO** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="e01d1-220">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="e01d1-221">c.</span><span class="sxs-lookup"><span data-stu-id="e01d1-221">c.</span></span> <span data-ttu-id="e01d1-222">**로그인 단추 이름** 형식 hello 이름 단추의 조직이 로그인 화면에 사용자가 toosee hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-222">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="e01d1-223">d.</span><span class="sxs-lookup"><span data-stu-id="e01d1-223">d.</span></span> <span data-ttu-id="e01d1-224">**SAML 사용자 ID 위치** 선택 **hello hello Subject 문의 NameIdentifier 요소에 사용자 ID가** 또는 **사용자 ID는 Attribute 요소에**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-224">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="e01d1-225">이 ID는 toobe hello JIRA 사용자 id가 있습니다. Hello 사용자 id 일치 하지 않는 경우 시스템에서 사용자가 toolog를 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-225">This ID has toobe hello JIRA user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="e01d1-226">e.</span><span class="sxs-lookup"><span data-stu-id="e01d1-226">e.</span></span> <span data-ttu-id="e01d1-227">선택 하는 경우 **사용자 ID는 Attribute 요소에** 옵션을 선택한 다음 **특성 이름** 사용자 Id가 예상한 것 hello 특성의 형식 hello 이름 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-227">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="e01d1-228">f.</span><span class="sxs-lookup"><span data-stu-id="e01d1-228">f.</span></span> <span data-ttu-id="e01d1-229">Hello 페더레이션된 도메인 (예: ADFS 등)와 Azure AD를 사용 하는 경우 클릭 hello **사용 홈 영역 검색** hello 구성 및 옵션 **도메인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-229">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="e01d1-230">g.</span><span class="sxs-lookup"><span data-stu-id="e01d1-230">g.</span></span> <span data-ttu-id="e01d1-231">**도메인 이름** hello 도메인 이름 입력 hello ADFS 기반 로그인의 경우.</span><span class="sxs-lookup"><span data-stu-id="e01d1-231">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="e01d1-232">h.</span><span class="sxs-lookup"><span data-stu-id="e01d1-232">h.</span></span> <span data-ttu-id="e01d1-233">확인 **사용 Single Sign-out** 시 사용자가 로그 JIRA에서 Azure AD에서 toolog 아웃 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="e01d1-233">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="e01d1-234">i.</span><span class="sxs-lookup"><span data-stu-id="e01d1-234">i.</span></span> <span data-ttu-id="e01d1-235">클릭 **저장** toosave hello 설정 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-235">Click **Save** button toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="e01d1-236">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="e01d1-236">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e01d1-237">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="e01d1-237">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e01d1-238">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e01d1-238">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e01d1-239">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e01d1-239">Creating an Azure AD test user</span></span>
<span data-ttu-id="e01d1-240">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-240">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="e01d1-242">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e01d1-242">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e01d1-243">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-243">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e01d1-245">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-245">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e01d1-247">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-247">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e01d1-249">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-249">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e01d1-251">a.</span><span class="sxs-lookup"><span data-stu-id="e01d1-251">a.</span></span> <span data-ttu-id="e01d1-252">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-252">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e01d1-253">b.</span><span class="sxs-lookup"><span data-stu-id="e01d1-253">b.</span></span> <span data-ttu-id="e01d1-254">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-254">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e01d1-255">c.</span><span class="sxs-lookup"><span data-stu-id="e01d1-255">c.</span></span> <span data-ttu-id="e01d1-256">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-256">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e01d1-257">d.</span><span class="sxs-lookup"><span data-stu-id="e01d1-257">d.</span></span> <span data-ttu-id="e01d1-258">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-258">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="e01d1-259">JIRA SAML SSO by Microsoft 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e01d1-259">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="e01d1-260">tooenable Azure AD 사용자가 toolog tooJIRA 온-프레미스 서버에서 이러한 해야에 프로 비전 JIRA SAML SSO Microsoft에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-260">tooenable Azure AD users toolog in tooJIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="e01d1-261">JIRA SAML SSO by Microsoft의 경우 프로비전이 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-261">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="e01d1-262">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e01d1-262">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e01d1-263">관리자 권한으로 JIRA 온-프레미스 서버 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-263">Log in tooyour JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="e01d1-264">Hello를 누르고 선 위에 마우스를 가져가면 **사용자 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-264">Hover on cog and click hello **User management**.</span></span>

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="e01d1-266">리디렉션된 tooAdministrator 액세스 페이지 tooenter는 **암호** 클릭 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-266">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="e01d1-268">**사용자 관리** 탭 섹션 아래에서  **사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-268">Under **User management** tab section, click **create user**.</span></span>

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="e01d1-270">Hello에 **"새 사용자 만들기"** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-270">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![직원 추가](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="e01d1-272">a.</span><span class="sxs-lookup"><span data-stu-id="e01d1-272">a.</span></span> <span data-ttu-id="e01d1-273">Hello에 **전자 메일 주소** textbox, 사용자의 hello 전자 메일 주소를 입력 같은 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-273">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="e01d1-274">b.</span><span class="sxs-lookup"><span data-stu-id="e01d1-274">b.</span></span> <span data-ttu-id="e01d1-275">Hello에 **전체 이름을** 텍스트 형식 Britta Simon 같은 hello 사용자의 전체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-275">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="e01d1-276">c.</span><span class="sxs-lookup"><span data-stu-id="e01d1-276">c.</span></span> <span data-ttu-id="e01d1-277">Hello에 **Username** 텍스트 형식 hello 전자 메일 사용자의 같은 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-277">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="e01d1-278">d.</span><span class="sxs-lookup"><span data-stu-id="e01d1-278">d.</span></span> <span data-ttu-id="e01d1-279">Hello에 **암호** textbox, 사용자의 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-279">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="e01d1-280">e.</span><span class="sxs-lookup"><span data-stu-id="e01d1-280">e.</span></span> <span data-ttu-id="e01d1-281">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-281">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e01d1-282">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-282">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e01d1-283">이 섹션에서는 액세스 tooJIRA Microsoft에서 SAML SSO를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-283">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJIRA SAML SSO by Microsoft.</span></span>

![사용자 할당][200] 

<span data-ttu-id="e01d1-285">**tooassign Britta Simon tooJIRA microsoft에서 SAML SSO hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e01d1-285">**tooassign Britta Simon tooJIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="e01d1-286">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-286">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="e01d1-288">Hello 응용 프로그램 목록에서 선택 **Microsoft에서 JIRA SAML SSO**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-288">In hello applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="e01d1-290">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-290">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="e01d1-292">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-292">Click **Add** button.</span></span> <span data-ttu-id="e01d1-293">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-293">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="e01d1-295">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-295">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e01d1-296">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-296">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e01d1-297">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-297">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e01d1-298">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="e01d1-298">Testing single sign-on</span></span>

<span data-ttu-id="e01d1-299">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-299">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e01d1-300">Microsoft 타일 hello 액세스 패널에에서 의해 hello JIRA SAML SSO를 클릭할 때 자동으로 로그온 tooyour JIRA SAML SSO Microsoft 응용 프로그램에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-300">When you click hello JIRA SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="e01d1-301">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e01d1-301">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e01d1-302">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e01d1-302">Additional resources</span></span>

* [<span data-ttu-id="e01d1-303">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="e01d1-303">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e01d1-304">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e01d1-304">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png


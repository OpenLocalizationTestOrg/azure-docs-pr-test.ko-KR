---
title: "자습서: SAML SSO for Jira by resolution GmbH와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 Jira GmbH 확인에 대 한 SAML SSO 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="c6adf-103">자습서: SAML SSO for Jira by resolution GmbH와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c6adf-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="c6adf-104">이 자습서에 설명 어떻게 toointegrate SAML SSO Jira에 대 한 Azure Active Directory (Azure AD)와 GmbH 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-104">In this tutorial, you learn how toointegrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c6adf-105">SAML SSO Jira에 대 한 Azure AD와 GmbH 해상도 따라 통합 이점을 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="c6adf-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c6adf-106">Jira에 대 한 확인 GmbH 액세스 tooSAML SSO 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-106">You can control in Azure AD who has access tooSAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="c6adf-107">사용 하면 사용자가 tooautomatically get 로그온 tooSAML SSO Jira 해상도 GmbH (Single Sign-on)는 Azure AD 계정 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c6adf-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c6adf-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c6adf-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6adf-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c6adf-110">Prerequisites</span></span>

<span data-ttu-id="c6adf-111">확인 GmbH Jira에 대 한 SAML SSO와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-111">tooconfigure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="c6adf-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c6adf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6adf-113">SAML SSO for Jira by resolution GmbH Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c6adf-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c6adf-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c6adf-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6adf-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c6adf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c6adf-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c6adf-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c6adf-118">Scenario description</span></span>
<span data-ttu-id="c6adf-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c6adf-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6adf-121">Hello 갤러리에서 Jira에 대 한 SAML SSO GmbH 해상도 따라 추가</span><span class="sxs-lookup"><span data-stu-id="c6adf-121">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="c6adf-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c6adf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="c6adf-123">Hello 갤러리에서 Jira에 대 한 SAML SSO GmbH 해상도 따라 추가</span><span class="sxs-lookup"><span data-stu-id="c6adf-123">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
<span data-ttu-id="c6adf-124">tooconfigure hello와의 통합 Jira에 대 한 SAML SSO GmbH 해상도 따라 Azure AD로 필요 tooadd SAML SSO Jira GmbH 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-124">tooconfigure hello integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need tooadd SAML SSO for Jira by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c6adf-125">**GmbH hello 갤러리에서 해상도 따라 Jira에 대 한 SAML SSO tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c6adf-125">**tooadd SAML SSO for Jira by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6adf-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c6adf-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c6adf-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c6adf-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c6adf-133">Hello 검색 상자에 입력 **Jira GmbH 확인에 대 한 SAML SSO**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-133">In hello search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="c6adf-135">Hello 결과 패널에서 선택 **Jira GmbH 확인에 대 한 SAML SSO**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-135">In hello results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c6adf-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c6adf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c6adf-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 SAML SSO for Jira by resolution GmbH에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c6adf-139">Single sign on toowork에 대 한 Azure AD tooknow GmbH가 tooa 사용자 Azure AD에서 해상도 따라 Jira에 대 한 SAML SSO에서 어떤 hello 테이블에 해당 사용자는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Jira by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="c6adf-140">즉, Azure AD 사용자 및 해상도 따라 Jira에 대 한 SAML SSO에서 hello 관련된 사용자 간 링크 관계를 GmbH toobe 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Jira by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="c6adf-141">Jira GmbH 확인에 대 한 SAML sso에서는 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-141">In SAML SSO for Jira by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c6adf-142">tooconfigure 및 Azure AD에서 single sign-on SAML sso에 대 한 테스트 Jira GmbH 해상도 따라 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c6adf-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c6adf-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6adf-145">**[Jira 해상도 GmbH 테스트 사용자에 대 한 SAML SSO 만들기](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave 확인은 사용자의 연결 된 Azure AD toohello 표현 GmbH Britta Simon Jira에 대 한 SAML SSO에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c6adf-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6adf-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="c6adf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c6adf-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c6adf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c6adf-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 확인 GmbH 응용 프로그램에서 single sign on Jira 프로그램 SAML SSO에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="c6adf-150">**확인, GmbH Jira에 대 한 SAML SSO와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c6adf-150">**tooconfigure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6adf-151">Hello hello에 Azure 포털에서에서 **Jira GmbH 확인에 대 한 SAML SSO** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-151">In hello Azure portal, on hello **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c6adf-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="c6adf-155">Hello에 **Jira 확인 GmbH 도메인 및 Url에 대 한 SAML SSO** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="c6adf-155">On hello **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="c6adf-157">a.</span><span class="sxs-lookup"><span data-stu-id="c6adf-157">a.</span></span> <span data-ttu-id="c6adf-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="c6adf-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="c6adf-159">b.</span><span class="sxs-lookup"><span data-stu-id="c6adf-159">b.</span></span> <span data-ttu-id="c6adf-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="c6adf-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="c6adf-161">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="c6adf-162">Tooconfigure hello 응용 프로그램에 필요한 경우 **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="c6adf-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="c6adf-164">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="c6adf-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c6adf-165">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-165">These values are not real.</span></span> <span data-ttu-id="c6adf-166">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c6adf-167">연락처 [Jira 확인 GmbH 클라이언트에 대 한 SAML SSO 지원 팀](https://www.resolution.de/go/support) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="c6adf-168">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="c6adf-170">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-170">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c6adf-172">다른 웹 브라우저 창에서 tooyour에 로그인 **해상도 GmbH 관리자 포털에서 Jira에 대 한 SAML SSO** 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-172">In a different web browser window, log in tooyour **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="c6adf-173">Hello를 누르고 선 위에 마우스를 가져가면 **추가 기능**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="c6adf-175">리디렉션된 tooAdministrator 액세스 페이지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="c6adf-176">Hello 입력 **암호** 클릭 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-176">Enter hello **Password** and click **Confirm** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="c6adf-178">[추가 기능] 탭 섹션에서 **새 추가 기능 찾기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="c6adf-179">검색 **SAML 로그인에 대해 SSO (Single) JIRA** 클릭 **설치** 단추 tooinstall hello 새 SAML 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="c6adf-181">hello 플러그 인 설치가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-181">hello plugin installation will start.</span></span> <span data-ttu-id="c6adf-182">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-182">Click **Close**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="c6adf-185">**관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-185">Click **Manage**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="c6adf-187">클릭 **구성** tooconfigure hello 새 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-187">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="c6adf-189">**SAML SingleSignOn 플러그 인 구성** 페이지 **추가 Id 공급자 추가** Id 공급자의 tooconfigure hello 설정 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="c6adf-191">이 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-191">Perform following steps on this page:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="c6adf-193">a.</span><span class="sxs-lookup"><span data-stu-id="c6adf-193">a.</span></span> <span data-ttu-id="c6adf-194">추가 **이름** 의 hello Id 공급자 (예: Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6adf-194">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="c6adf-195">b.</span><span class="sxs-lookup"><span data-stu-id="c6adf-195">b.</span></span> <span data-ttu-id="c6adf-196">추가 **설명** 의 hello Id 공급자 (예: Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6adf-196">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="c6adf-197">c.</span><span class="sxs-lookup"><span data-stu-id="c6adf-197">c.</span></span> <span data-ttu-id="c6adf-198">클릭 **XML** 및 선택 hello **메타 데이터** Azure 포털에서 다운로드 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-198">Click **XML** and select hello **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="c6adf-199">d.</span><span class="sxs-lookup"><span data-stu-id="c6adf-199">d.</span></span> <span data-ttu-id="c6adf-200">**로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-200">Click **Load** button.</span></span>

    <span data-ttu-id="c6adf-201">e.</span><span class="sxs-lookup"><span data-stu-id="c6adf-201">e.</span></span> <span data-ttu-id="c6adf-202">Hello IdP 메타 데이터 읽고 hello 스크린샷에 강조 표시 된 대로 hello 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-202">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   

16. <span data-ttu-id="c6adf-203">클릭 **설정을 저장** toosave hello 설정 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-203">Click **Save settings** button toosave hello settings.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="c6adf-205">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="c6adf-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c6adf-206">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="c6adf-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c6adf-207">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c6adf-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c6adf-208">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c6adf-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="c6adf-209">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c6adf-211">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c6adf-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6adf-212">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c6adf-214">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c6adf-216">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c6adf-218">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c6adf-220">a.</span><span class="sxs-lookup"><span data-stu-id="c6adf-220">a.</span></span> <span data-ttu-id="c6adf-221">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6adf-222">b.</span><span class="sxs-lookup"><span data-stu-id="c6adf-222">b.</span></span> <span data-ttu-id="c6adf-223">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c6adf-224">c.</span><span class="sxs-lookup"><span data-stu-id="c6adf-224">c.</span></span> <span data-ttu-id="c6adf-225">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c6adf-226">d.</span><span class="sxs-lookup"><span data-stu-id="c6adf-226">d.</span></span> <span data-ttu-id="c6adf-227">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="c6adf-228">SAML SSO for Jira by resolution GmbH 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c6adf-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="c6adf-229">tooenable Azure AD 사용자가 toolog tooSAML Jira에 대 한 SSO GmbH 해상도 따라,에서 이러한 해야에 프로 비전 Jira에 대 한 SAML SSO GmbH 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-229">tooenable Azure AD users toolog in tooSAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="c6adf-230">SAML SSO for Jira by resolution GmbH에서 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="c6adf-231">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c6adf-231">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6adf-232">Tooyour Jira 해상도 GmbH 회사 사이트에 대 한 관리자 권한으로 SAML SSO 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-232">Log in tooyour SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="c6adf-233">Hello를 누르고 선 위에 마우스를 가져가면 **사용자 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-233">Hover on cog and click hello **User management**.</span></span>

    ![직원 추가](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="c6adf-235">리디렉션된 tooAdministrator 액세스 페이지 tooenter는 **암호** 클릭 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-235">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![직원 추가](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="c6adf-237">**사용자 관리** 탭 섹션 아래에서  **사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-237">Under **User management** tab section, click **create user**.</span></span>

    ![직원 추가](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="c6adf-239">Hello에 **"새 사용자 만들기"** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-239">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![직원 추가](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="c6adf-241">a.</span><span class="sxs-lookup"><span data-stu-id="c6adf-241">a.</span></span> <span data-ttu-id="c6adf-242">Hello에 **전자 메일 주소** textbox, 사용자의 hello 전자 메일 주소를 입력 같은 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-242">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="c6adf-243">b.</span><span class="sxs-lookup"><span data-stu-id="c6adf-243">b.</span></span> <span data-ttu-id="c6adf-244">Hello에 **전체 이름을** 텍스트 형식 Britta Simon 같은 hello 사용자의 전체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-244">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="c6adf-245">c.</span><span class="sxs-lookup"><span data-stu-id="c6adf-245">c.</span></span> <span data-ttu-id="c6adf-246">Hello에 **Username** 텍스트 형식 hello 전자 메일 사용자의 같은 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-246">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="c6adf-247">d.</span><span class="sxs-lookup"><span data-stu-id="c6adf-247">d.</span></span> <span data-ttu-id="c6adf-248">Hello에 **암호** textbox, 사용자의 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-248">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="c6adf-249">e.</span><span class="sxs-lookup"><span data-stu-id="c6adf-249">e.</span></span> <span data-ttu-id="c6adf-250">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-250">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c6adf-251">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c6adf-252">이 섹션에서는 GmbH 해상도 따라 액세스 tooSAML SSO Jira에 대 한 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Jira by resolution GmbH.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c6adf-254">**tooassign GmbH, 해상도 따라 Britta Simon tooSAML Jira에 대 한 SSO hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c6adf-254">**tooassign Britta Simon tooSAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6adf-255">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c6adf-257">Hello 응용 프로그램 목록에서 선택 **Jira GmbH 확인에 대 한 SAML SSO**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-257">In hello applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="c6adf-259">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c6adf-261">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-261">Click **Add** button.</span></span> <span data-ttu-id="c6adf-262">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c6adf-264">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c6adf-265">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c6adf-266">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c6adf-267">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c6adf-267">Testing single sign-on</span></span>

<span data-ttu-id="c6adf-268">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c6adf-269">Hello 액세스 패널에서에서 GmbH 타일을 확인 하 여 hello Jira에 대 한 SAML SSO를 클릭할 때 가져와야 자동으로 로그온 tooyour SAML SSO Jira에 대 한 GmbH 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6adf-269">When you click hello SAML SSO for Jira by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="c6adf-270">액세스 패널에 대한 자세한 내용은 [Azure 시작](active-directory-saas-access-panel-introduction.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6adf-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c6adf-271">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c6adf-271">Additional resources</span></span>

* [<span data-ttu-id="c6adf-272">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="c6adf-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6adf-273">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c6adf-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png


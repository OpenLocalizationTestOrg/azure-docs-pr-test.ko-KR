---
title: "자습서: SAML SSO for Confluence by resolution GmbH와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 합류 GmbH 확인에 대 한 SAML SSO 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: fe50636709857ec49023e24bdc8c6cd8c58e3c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="2abbb-103">자습서: SAML SSO for Confluence by resolution GmbH와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2abbb-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="2abbb-104">이 자습서에 설명 어떻게 toointegrate SAML SSO 합류에 대 한 Azure Active Directory (Azure AD)와 GmbH 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-104">In this tutorial, you learn how toointegrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2abbb-105">SAML SSO 합류에 대 한 Azure AD와 GmbH 해상도 따라 통합 이점을 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="2abbb-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2abbb-106">확인 GmbH 합류에 대 한 SSO 액세스 tooSAML을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-106">You can control in Azure AD who has access tooSAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="2abbb-107">에 사용자가 tooautomatically get 로그온 tooSAML 합류에 대 한 SSO 해상도 GmbH (Single Sign-on)는 Azure AD 계정 사용 하 여 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2abbb-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2abbb-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2abbb-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2abbb-110">Prerequisites</span></span>

<span data-ttu-id="2abbb-111">확인 GmbH 합류에 대 한 SAML SSO와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-111">tooconfigure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="2abbb-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2abbb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2abbb-113">SAML SSO for Confluence by resolution GmbH Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2abbb-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2abbb-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2abbb-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2abbb-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2abbb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2abbb-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2abbb-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2abbb-118">Scenario description</span></span>
<span data-ttu-id="2abbb-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2abbb-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2abbb-121">Hello 갤러리에서 합류에 대 한 SAML SSO GmbH 해상도 따라 추가</span><span class="sxs-lookup"><span data-stu-id="2abbb-121">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="2abbb-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2abbb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="2abbb-123">Hello 갤러리에서 합류에 대 한 SAML SSO GmbH 해상도 따라 추가</span><span class="sxs-lookup"><span data-stu-id="2abbb-123">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>

<span data-ttu-id="2abbb-124">tooconfigure hello와의 통합에 대 한 일련의 SAML SSO GmbH 해상도 따라 Azure AD로 필요 tooadd SAML SSO 합류 GmbH 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-124">tooconfigure hello integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need tooadd SAML SSO for Confluence by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2abbb-125">**GmbH hello 갤러리에서 해상도 따라 합류에 대 한 SAML SSO tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2abbb-125">**tooadd SAML SSO for Confluence by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2abbb-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2abbb-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2abbb-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="2abbb-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="2abbb-133">Hello 검색 상자에 입력 **합류 GmbH 확인에 대 한 SAML SSO**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-133">In hello search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. <span data-ttu-id="2abbb-135">Hello 결과 패널에서 선택 **합류 GmbH 확인에 대 한 SAML SSO**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-135">In hello results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2abbb-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2abbb-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="2abbb-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 SAML SSO for Confluence by resolution GmbH에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2abbb-139">Single sign on toowork에 대 한 Azure AD tooknow GmbH가 tooa 사용자 Azure AD에서 해상도 따라 합류에 대 한 SAML SSO에서 어떤 hello 테이블에 해당 사용자는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Confluence by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="2abbb-140">즉, Azure AD 사용자 및 해상도 따라 SAML SSO에 대 한 일련의 hello 관련된 사용자 간 링크 관계를 GmbH toobe 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Confluence by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="2abbb-141">합류 GmbH 확인에 대 한 SAML sso에서는 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-141">In SAML SSO for Confluence by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2abbb-142">tooconfigure 및 Azure AD에서 single sign-on SAML sso에 대 한 테스트 합류 GmbH 해상도 따라 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2abbb-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2abbb-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2abbb-145">**[합류 해상도 GmbH 테스트 사용자에 대 한 SAML SSO 만들기](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  -toohave 확인은 사용자의 연결 된 Azure AD toohello 표현 GmbH Britta Simon 합류에 대 한 SAML SSO에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2abbb-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2abbb-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="2abbb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2abbb-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2abbb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2abbb-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 확인 GmbH 응용 프로그램에서 single sign on 합류 프로그램 SAML SSO에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="2abbb-150">**확인 GmbH, 합류에 대 한 SAML SSO와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2abbb-150">**tooconfigure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="2abbb-151">Hello hello에 Azure 포털에서에서 **합류 GmbH 확인에 대 한 SAML SSO** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-151">In hello Azure portal, on hello **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="2abbb-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. <span data-ttu-id="2abbb-155">Hello에 **합류 확인 GmbH 도메인 및 Url에 대 한 SAML SSO** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="2abbb-155">On hello **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="2abbb-157">a.</span><span class="sxs-lookup"><span data-stu-id="2abbb-157">a.</span></span> <span data-ttu-id="2abbb-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="2abbb-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="2abbb-159">b.</span><span class="sxs-lookup"><span data-stu-id="2abbb-159">b.</span></span> <span data-ttu-id="2abbb-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="2abbb-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="2abbb-161">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2abbb-162">Tooconfigure hello 응용 프로그램에 필요한 경우 **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="2abbb-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="2abbb-164">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="2abbb-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2abbb-165">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-165">These values are not real.</span></span> <span data-ttu-id="2abbb-166">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2abbb-167">연락처 [합류 확인 GmbH 클라이언트에 대 한 SAML SSO 지원 팀](https://www.resolution.de/go/support) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="2abbb-168">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. <span data-ttu-id="2abbb-170">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-170">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. <span data-ttu-id="2abbb-172">다른 웹 브라우저 창에서 tooyour에 로그인 **해상도 GmbH 관리자 포털에서 합류에 대 한 SAML SSO** 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-172">In a different web browser window, log in tooyour **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="2abbb-173">Hello를 누르고 선 위에 마우스를 가져가면 **추가 기능**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. <span data-ttu-id="2abbb-175">리디렉션된 tooAdministrator 액세스 페이지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="2abbb-176">Hello 암호를 입력 하 고 클릭 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-176">Enter hello password and click **Confirm** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. <span data-ttu-id="2abbb-178">**ATLASSIAN MARKETPLACE** 탭 아래에서 **새 추가 기능 찾기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. <span data-ttu-id="2abbb-180">검색 **SAML 로그인에 대해 SSO (Single) 합류** 클릭 **설치** 단추 tooinstall hello 새 SAML 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. <span data-ttu-id="2abbb-182">hello 플러그 인 설치가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-182">hello plugin installation will start.</span></span> <span data-ttu-id="2abbb-183">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-183">Click **Close**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. <span data-ttu-id="2abbb-186">**관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-186">Click **Manage**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. <span data-ttu-id="2abbb-188">클릭 **구성** tooconfigure hello 새 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-188">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. <span data-ttu-id="2abbb-190">또한 새로운 이 플러그 인은 **사용자 및 보안** 탭 아래에도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. <span data-ttu-id="2abbb-192">**SAML SingleSignOn 플러그 인 구성** 페이지 **추가 Id 공급자 추가** Id 공급자의 tooconfigure hello 설정 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. <span data-ttu-id="2abbb-194">이 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-194">Perform following steps on this page:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    <span data-ttu-id="2abbb-196">a.</span><span class="sxs-lookup"><span data-stu-id="2abbb-196">a.</span></span> <span data-ttu-id="2abbb-197">추가 **이름** 의 hello Id 공급자 (예: Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2abbb-197">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="2abbb-198">b.</span><span class="sxs-lookup"><span data-stu-id="2abbb-198">b.</span></span> <span data-ttu-id="2abbb-199">추가 **설명** 의 hello Id 공급자 (예: Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2abbb-199">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="2abbb-200">c.</span><span class="sxs-lookup"><span data-stu-id="2abbb-200">c.</span></span> <span data-ttu-id="2abbb-201">클릭 **XML** 및 선택 hello **메타 데이터** Azure 포털에서 다운로드 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-201">Click **XML** and select hello **Metadata** file that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="2abbb-202">d.</span><span class="sxs-lookup"><span data-stu-id="2abbb-202">d.</span></span> <span data-ttu-id="2abbb-203">**로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-203">Click **Load** button.</span></span>

    <span data-ttu-id="2abbb-204">e.</span><span class="sxs-lookup"><span data-stu-id="2abbb-204">e.</span></span> <span data-ttu-id="2abbb-205">Hello IdP 메타 데이터 읽고 hello 스크린샷에 강조 표시 된 대로 hello 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-205">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   
18. <span data-ttu-id="2abbb-206">클릭 **설정을 저장** toosave hello 설정 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-206">Click **Save settings** button toosave hello settings.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="2abbb-208">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="2abbb-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2abbb-209">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="2abbb-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2abbb-210">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2abbb-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2abbb-211">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2abbb-211">Creating an Azure AD test user</span></span>
<span data-ttu-id="2abbb-212">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="2abbb-214">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2abbb-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2abbb-215">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-215">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2abbb-217">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-217">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2abbb-219">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-219">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2abbb-221">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-221">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2abbb-223">a.</span><span class="sxs-lookup"><span data-stu-id="2abbb-223">a.</span></span> <span data-ttu-id="2abbb-224">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-224">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2abbb-225">b.</span><span class="sxs-lookup"><span data-stu-id="2abbb-225">b.</span></span> <span data-ttu-id="2abbb-226">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-226">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2abbb-227">c.</span><span class="sxs-lookup"><span data-stu-id="2abbb-227">c.</span></span> <span data-ttu-id="2abbb-228">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-228">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2abbb-229">d.</span><span class="sxs-lookup"><span data-stu-id="2abbb-229">d.</span></span> <span data-ttu-id="2abbb-230">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-230">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="2abbb-231">SAML SSO for Confluence by resolution GmbH 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2abbb-231">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="2abbb-232">tooenable Azure AD 사용자가 toolog tooSAML 합류에 대 한 SSO GmbH 해상도 따라,에서 이러한 해야에 프로 비전 합류에 대 한 SAML SSO GmbH 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-232">tooenable Azure AD users toolog in tooSAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="2abbb-233">SAML SSO for Confluence by resolution GmbH에서 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-233">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="2abbb-234">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2abbb-234">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2abbb-235">Tooyour 합류 해상도 GmbH 회사 사이트에 대 한 관리자 권한으로 SAML SSO 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-235">Log in tooyour SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="2abbb-236">Hello를 누르고 선 위에 마우스를 가져가면 **사용자 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-236">Hover on cog and click hello **User management**.</span></span>

    ![직원 추가](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. <span data-ttu-id="2abbb-238">[사용자] 섹션에서 **사용자 추가** 탭을 클릭합니다. Hello에 **"사용자 추가"** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-238">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![직원 추가](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="2abbb-240">a.</span><span class="sxs-lookup"><span data-stu-id="2abbb-240">a.</span></span> <span data-ttu-id="2abbb-241">Hello에 **Username** Britta Simon와 같은 사용자의 형식 hello 전자 메일 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-241">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="2abbb-242">b.</span><span class="sxs-lookup"><span data-stu-id="2abbb-242">b.</span></span> <span data-ttu-id="2abbb-243">Hello에 **전체 이름을** 텍스트 형식 hello Britta Simon와 같은 사용자의 전체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-243">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="2abbb-244">c.</span><span class="sxs-lookup"><span data-stu-id="2abbb-244">c.</span></span> <span data-ttu-id="2abbb-245">Hello에 **전자 메일** textbox, 사용자의 hello 전자 메일 주소를 입력 같은 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-245">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="2abbb-246">d.</span><span class="sxs-lookup"><span data-stu-id="2abbb-246">d.</span></span> <span data-ttu-id="2abbb-247">Hello에 **암호** textbox Britta Simon에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-247">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="2abbb-248">e.</span><span class="sxs-lookup"><span data-stu-id="2abbb-248">e.</span></span> <span data-ttu-id="2abbb-249">클릭 **암호 확인** hello 암호를 다시 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-249">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="2abbb-250">f.</span><span class="sxs-lookup"><span data-stu-id="2abbb-250">f.</span></span> <span data-ttu-id="2abbb-251">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-251">Click **Add** button.</span></span>    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2abbb-252">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2abbb-253">이 섹션에서는 확인 GmbH 합류에 대 한 SSO 액세스 tooSAML 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Confluence by resolution GmbH.</span></span>

![사용자 할당][200] 

<span data-ttu-id="2abbb-255">**tooassign GmbH, 해상도 따라 Britta Simon tooSAML 합류에 대 한 SSO hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2abbb-255">**tooassign Britta Simon tooSAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="2abbb-256">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2abbb-258">Hello 응용 프로그램 목록에서 선택 **합류 GmbH 확인에 대 한 SAML SSO**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-258">In hello applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. <span data-ttu-id="2abbb-260">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="2abbb-262">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-262">Click **Add** button.</span></span> <span data-ttu-id="2abbb-263">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="2abbb-265">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2abbb-266">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2abbb-267">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2abbb-268">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2abbb-268">Testing single sign-on</span></span>

<span data-ttu-id="2abbb-269">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-269">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2abbb-270">Hello 액세스 패널에서에서 GmbH 타일을 확인 하 여 hello 합류에 대 한 SAML SSO를 클릭할 때 가져와야 자동으로 로그온 tooyour SAML SSO 합류에 대 한 GmbH 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2abbb-270">When you click hello SAML SSO for Confluence by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="2abbb-271">액세스 패널에 대한 자세한 내용은 [Azure 시작](active-directory-saas-access-panel-introduction.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2abbb-271">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2abbb-272">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2abbb-272">Additional resources</span></span>

* [<span data-ttu-id="2abbb-273">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="2abbb-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2abbb-274">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2abbb-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png


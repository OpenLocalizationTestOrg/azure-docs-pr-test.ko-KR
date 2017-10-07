---
title: "자습서: Land Gorilla Client와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 토지 고릴라 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: e95a30551e636108fe22a7ab6d1827bc12d7f9a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="b612c-103">자습서: Land Gorilla Client와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b612c-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="b612c-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)를 사용 하 여 토지 고릴라 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-104">In this tutorial, you learn how toointegrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b612c-105">토지 고릴라 클라이언트를 Azure AD와 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-105">Integrating Land Gorilla Client with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b612c-106">액세스 tooLand 고릴라 클라이언트에 게 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-106">You can control in Azure AD who has access tooLand Gorilla Client</span></span>
- <span data-ttu-id="b612c-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooLand 고릴라 클라이언트 (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-107">You can enable your users tooautomatically get signed-on tooLand Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b612c-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="b612c-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b612c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b612c-110">Prerequisites</span></span>

<span data-ttu-id="b612c-111">토지 고릴라 클라이언트와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-111">tooconfigure Azure AD integration with Land Gorilla Client, you need hello following items:</span></span>

- <span data-ttu-id="b612c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b612c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b612c-113">Land Gorilla Client Single Sign-On을 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b612c-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="b612c-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="b612c-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b612c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b612c-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="b612c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b612c-118">Scenario description</span></span>
<span data-ttu-id="b612c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b612c-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b612c-121">Hello 갤러리에서 토지 고릴라 클라이언트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-121">Adding Land Gorilla Client from hello gallery</span></span>
2. <span data-ttu-id="b612c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b612c-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-hello-gallery"></a><span data-ttu-id="b612c-123">Hello 갤러리에서 토지 고릴라 클라이언트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-123">Adding Land Gorilla Client from hello gallery</span></span>
<span data-ttu-id="b612c-124">tooconfigure hello와의 통합 토지 고릴라 클라이언트 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd 토지 고릴라 클라이언트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-124">tooconfigure hello integration of Land Gorilla Client into Azure AD, you need tooadd Land Gorilla Client from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b612c-125">**tooadd hello 갤러리에서 토지 고릴라 클라이언트 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b612c-125">**tooadd Land Gorilla Client from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b612c-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b612c-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b612c-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b612c-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b612c-133">Hello 검색 상자에 입력 **토지 고릴라 클라이언트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-133">In hello search box, type **Land Gorilla Client**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="b612c-135">Hello 결과 패널에서 선택 **토지 고릴라 클라이언트**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-135">In hello results panel, select **Land Gorilla Client**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b612c-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b612c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b612c-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Land Gorilla Client에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b612c-139">Single sign on toowork에 대 한 Azure AD는 tooknow 토지 고릴라 클라이언트에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Land Gorilla Client is tooa user in Azure AD.</span></span> <span data-ttu-id="b612c-140">즉, Azure AD 사용자 및 토지 고릴라 클라이언트에서 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-140">In other words, a link relationship between an Azure AD user and hello related user in Land Gorilla Client needs toobe established.</span></span>

<span data-ttu-id="b612c-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** 토지 고릴라 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="b612c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="b612c-142">tooconfigure 및 토지 고릴라 클라이언트를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-142">tooconfigure and test Azure AD single sign-on with Land Gorilla Client, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b612c-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b612c-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on 제한 된 그룹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="b612c-145">**[토지 고릴라 테스트 사용자 만들기](#creating-a-land-gorilla-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="b612c-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b612c-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="b612c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b612c-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b612c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b612c-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 토지 고릴라 클라이언트 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="b612c-150">**토지 고릴라 클라이언트와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b612c-150">**tooconfigure Azure AD single sign-on with Land Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="b612c-151">Hello에 hello Azure 관리 포털에서 **토지 고릴라 클라이언트** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-151">In hello Azure Management portal, on hello **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b612c-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="b612c-155">Hello에 **토지 고릴라 클라이언트 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-155">On hello **Land Gorilla Client Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="b612c-157">a.</span><span class="sxs-lookup"><span data-stu-id="b612c-157">a.</span></span> <span data-ttu-id="b612c-158">Hello에 **식별자** hello 패턴 중 하나를 사용 하 여 형식 hello 값 텍스트 상자:</span><span class="sxs-lookup"><span data-stu-id="b612c-158">In hello **Identifier** textbox, type hello value using one of hello following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="b612c-159">b.</span><span class="sxs-lookup"><span data-stu-id="b612c-159">b.</span></span> <span data-ttu-id="b612c-160">Hello에 **회신 URL** 텍스트 상자에 hello 패턴 중 하나를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="b612c-160">In hello **Reply URL** textbox, type a URL using one of hello following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="b612c-161">이러한 없는지 hello 실제 값 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b612c-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="b612c-162">Tooupdate hello 실제 식별자와 회신 URL 사용 하 여 이러한 값 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="b612c-163">여기 있습니다 toouse hello의 고유 값을 hello 식별자의에서 문자열을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="b612c-164">연락처 [토지 고릴라 클라이언트 팀](https://www.landgorilla.com/support/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="b612c-165">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="b612c-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-167">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="b612c-169">tooget SSO 구성 연락처 토지 고릴라 끝 응용 프로그램에 대 한 완료 [토지 고릴라 클라이언트 지원 팀](https://www.landgorilla.com/support/) hello 다운로드로 제공 **"메타 데이터 XML** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-169">tooget SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with hello downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b612c-170">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b612c-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="b612c-171">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-171">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b612c-173">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b612c-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b612c-174">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-174">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b612c-176">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-176">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b612c-178">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="b612c-178">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b612c-180">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b612c-182">a.</span><span class="sxs-lookup"><span data-stu-id="b612c-182">a.</span></span> <span data-ttu-id="b612c-183">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b612c-184">b.</span><span class="sxs-lookup"><span data-stu-id="b612c-184">b.</span></span> <span data-ttu-id="b612c-185">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b612c-186">c.</span><span class="sxs-lookup"><span data-stu-id="b612c-186">c.</span></span> <span data-ttu-id="b612c-187">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b612c-188">d.</span><span class="sxs-lookup"><span data-stu-id="b612c-188">d.</span></span> <span data-ttu-id="b612c-189">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="b612c-190">Land Gorilla 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b612c-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="b612c-191">와 협력 하세요 [토지 고릴라 지원 팀](https://www.landgorilla.com/support/) hello 토지 고릴라 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) tooadd hello users in hello Land Gorilla platform.</span></span>
    
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b612c-192">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b612c-193">이 섹션에서는 그녀의 액세스 tooLand 고릴라 클라이언트에 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLand Gorilla Client.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b612c-195">**tooassign Britta Simon tooLand 고릴라 클라이언트 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b612c-195">**tooassign Britta Simon tooLand Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="b612c-196">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-196">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b612c-198">Hello 응용 프로그램 목록에서 선택 **토지 고릴라 클라이언트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-198">In hello applications list, select **Land Gorilla Client**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="b612c-200">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b612c-202">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-202">Click **Add** button.</span></span> <span data-ttu-id="b612c-203">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b612c-205">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b612c-206">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b612c-207">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="b612c-208">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b612c-208">Testing single sign-on</span></span>

<span data-ttu-id="b612c-209">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b612c-210">Hello 액세스 패널에서에서 hello 토지 고릴라 클라이언트 타일을 클릭할 때 자동으로 로그온 tooyour 토지 고릴라 클라이언트 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b612c-210">When you click hello Land Gorilla Client tile in hello Access Panel, you should get automatically signed-on tooyour Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b612c-211">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b612c-211">Additional resources</span></span>

* [<span data-ttu-id="b612c-212">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="b612c-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b612c-213">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b612c-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png

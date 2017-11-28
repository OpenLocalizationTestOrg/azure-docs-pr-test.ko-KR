---
title: "자습서: Kantega SSO for Bamboo와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Bamboo에 대 한 SSO Kantega 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 8bf637ff440e8e3948db882861bee6e73f8aa879
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a><span data-ttu-id="2043a-103">자습서: Kantega SSO for Bamboo와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2043a-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo</span></span>

<span data-ttu-id="2043a-104">이 자습서에 설명 어떻게 toointegrate Kantega SSO Bamboo Azure Active directory (Azure AD)에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-104">In this tutorial, you learn how toointegrate Kantega SSO for Bamboo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2043a-105">다음 이점을 hello로 제공 Kantega SSO Bamboo에 대 한 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="2043a-105">Integrating Kantega SSO for Bamboo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2043a-106">Bamboo에 대 한 SSO 액세스 tooKantega을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-106">You can control in Azure AD who has access tooKantega SSO for Bamboo</span></span>
- <span data-ttu-id="2043a-107">프로그램 사용자 tooautomatically get 로그온 tooKantega SSO (Single Sign-on) 표시 하며 Bamboo에 대 한 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Bamboo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2043a-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2043a-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2043a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2043a-110">Prerequisites</span></span>

<span data-ttu-id="2043a-111">Bamboo에 대 한 Kantega SSO와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-111">tooconfigure Azure AD integration with Kantega SSO for Bamboo, you need hello following items:</span></span>

- <span data-ttu-id="2043a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2043a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2043a-113">Kantega SSO for Bamboo Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2043a-113">A Kantega SSO for Bamboo single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2043a-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2043a-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2043a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2043a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2043a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2043a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2043a-118">Scenario description</span></span>
<span data-ttu-id="2043a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2043a-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2043a-121">Bamboo에 대 한 SSO Kantega hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2043a-121">Adding Kantega SSO for Bamboo from hello gallery</span></span>
2. <span data-ttu-id="2043a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2043a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bamboo-from-hello-gallery"></a><span data-ttu-id="2043a-123">Bamboo에 대 한 SSO Kantega hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2043a-123">Adding Kantega SSO for Bamboo from hello gallery</span></span>
<span data-ttu-id="2043a-124">tooconfigure hello와의 통합 Kantega SSO Bamboo에 대 한 Azure AD로 필요 tooadd Kantega SSO Bamboo 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-124">tooconfigure hello integration of Kantega SSO for Bamboo into Azure AD, you need tooadd Kantega SSO for Bamboo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2043a-125">**Bamboo hello 갤러리에서에 대 한 SSO Kantega tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2043a-125">**tooadd Kantega SSO for Bamboo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2043a-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2043a-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2043a-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="2043a-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="2043a-133">Hello 검색 상자에 입력 **Bamboo에 대 한 SSO Kantega**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-133">In hello search box, type **Kantega SSO for Bamboo**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. <span data-ttu-id="2043a-135">Hello 결과 패널에서 선택 **Bamboo에 대 한 Kantega SSO**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-135">In hello results panel, select **Kantega SSO for Bamboo**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2043a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2043a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2043a-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Kantega SSO for Bamboo에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bamboo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2043a-139">Single sign on toowork에 대 한 Azure AD는 tooknow Bamboo에 대 한 Kantega SSO에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Bamboo is tooa user in Azure AD.</span></span> <span data-ttu-id="2043a-140">즉, Azure AD 사용자 및 hello Bamboo에 대 한 Kantega SSO에서 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Bamboo needs toobe established.</span></span>

<span data-ttu-id="2043a-141">Bamboo에 대 한 Kantega sso에서는 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-141">In Kantega SSO for Bamboo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2043a-142">tooconfigure와 Bamboo에 대 한 Kantega SSO와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Bamboo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2043a-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2043a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2043a-145">**[Bamboo 테스트 사용자에 대 한 Kantega SSO 만들기](#creating-a-kantega-sso-for-bamboo-test-user)**  -toohave Britta Simon Kantega SSO는 사용자의 연결 된 Azure AD toohello 표현 Bamboo에 대 한에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-145">**[Creating a Kantega SSO for Bamboo test user](#creating-a-kantega-sso-for-bamboo-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Bamboo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2043a-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2043a-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="2043a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2043a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2043a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2043a-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Bamboo 응용 프로그램에 대 한 프로그램 Kantega SSO에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Bamboo application.</span></span>

<span data-ttu-id="2043a-150">**Bamboo에 대 한 Kantega SSO와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2043a-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="2043a-151">Hello hello에 Azure 포털에서에서 **Bamboo에 대 한 Kantega SSO** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-151">In hello Azure portal, on hello **Kantega SSO for Bamboo** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="2043a-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. <span data-ttu-id="2043a-155">**IDP** 시작 모드 hello에 **Bamboo 도메인 및 Url에 대 한 SSO Kantega** 섹션 hello 단계 다음에 수행:</span><span class="sxs-lookup"><span data-stu-id="2043a-155">In **IDP** initiated mode, on hello **Kantega SSO for Bamboo Domain and URLs** section perform hello following step :</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    <span data-ttu-id="2043a-157">a.</span><span class="sxs-lookup"><span data-stu-id="2043a-157">a.</span></span> <span data-ttu-id="2043a-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2043a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="2043a-159">b.</span><span class="sxs-lookup"><span data-stu-id="2043a-159">b.</span></span> <span data-ttu-id="2043a-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2043a-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="2043a-161">**SP** 검사 시작된 모드 **고급 URL 설정 표시** hello 단계 다음에 수행:</span><span class="sxs-lookup"><span data-stu-id="2043a-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step :</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    <span data-ttu-id="2043a-163">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2043a-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2043a-164">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-164">These values are not real.</span></span> <span data-ttu-id="2043a-165">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2043a-166">이러한 값은 hello 자습서의 뒷부분에 설명 된 Bamboo 플러그 인의 hello 구성 하는 동안 수신 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-166">These values are recieved during hello configuration of Bamboo plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="2043a-167">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. <span data-ttu-id="2043a-169">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-169">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2043a-171">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Bamboo 프레미스 서버에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-171">In a different web browser window, log in tooyour Bamboo  on premise server as an administrator.</span></span>

8. <span data-ttu-id="2043a-172">Hello를 누르고 선 위에 마우스를 가져가면 **추가 기능**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. <span data-ttu-id="2043a-174">[추가 기능] 탭 섹션에서 **새 추가 기능 찾기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="2043a-175">검색 **Bamboo (SAML & Kerberos)에 대 한 Kantega SSO** 클릭 **설치** 단추 tooinstall hello 새 SAML 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-175">Search **Kantega SSO for Bamboo (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. <span data-ttu-id="2043a-177">hello 플러그 인 설치가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-177">hello plugin installation will start.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. <span data-ttu-id="2043a-179">한 번 hello 설치가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-179">Once hello installation is complete.</span></span> <span data-ttu-id="2043a-180">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-180">Click **Close**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. <span data-ttu-id="2043a-182">**관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-182">Click **Manage**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. <span data-ttu-id="2043a-184">클릭 **구성** tooconfigure hello 새 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-184">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. <span data-ttu-id="2043a-186">Hello에 **SAML** 섹션.</span><span class="sxs-lookup"><span data-stu-id="2043a-186">In hello **SAML** section.</span></span> <span data-ttu-id="2043a-187">선택 **Azure Active Directory (Azure AD)** hello에서 **추가 id 공급자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-187">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. <span data-ttu-id="2043a-189">구독 수준을 **기본**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-189">Select subscription level as **Basic**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. <span data-ttu-id="2043a-191">Hello에 **앱 속성** 섹션에서 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-191">On hello **App properties** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    <span data-ttu-id="2043a-193">a.</span><span class="sxs-lookup"><span data-stu-id="2043a-193">a.</span></span> <span data-ttu-id="2043a-194">복사 hello **앱 ID URI** 값으로 사용 하 여 **식별자, 회신 URL 및 로그온 URL** hello에 **Bamboo 도메인 및 Url에 대 한 SSO Kantega** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="2043a-194">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Bamboo Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="2043a-195">b.</span><span class="sxs-lookup"><span data-stu-id="2043a-195">b.</span></span> <span data-ttu-id="2043a-196">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-196">Click **Next**.</span></span>

17. <span data-ttu-id="2043a-197">Hello에 **메타 데이터 가져오기** 섹션에서 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-197">On hello **Metadata import** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    <span data-ttu-id="2043a-199">a.</span><span class="sxs-lookup"><span data-stu-id="2043a-199">a.</span></span> <span data-ttu-id="2043a-200">**Metadata file on my computer**(내 컴퓨터의 메타데이터 파일)를 클릭하여 Azure Portal에서 다운로드한 메타데이터 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-200">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="2043a-201">b.</span><span class="sxs-lookup"><span data-stu-id="2043a-201">b.</span></span> <span data-ttu-id="2043a-202">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-202">Click **Next**.</span></span>

18. <span data-ttu-id="2043a-203">Hello에 **이름과 SSO 위치** 섹션에서 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-203">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    <span data-ttu-id="2043a-205">a.</span><span class="sxs-lookup"><span data-stu-id="2043a-205">a.</span></span> <span data-ttu-id="2043a-206">Hello Id 공급자의 이름을 추가에서 **Id 공급자 이름** (예: Azure AD) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-206">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="2043a-207">b.</span><span class="sxs-lookup"><span data-stu-id="2043a-207">b.</span></span> <span data-ttu-id="2043a-208">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-208">Click **Next**.</span></span>

19. <span data-ttu-id="2043a-209">Hello 서명 인증서를 확인 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-209">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. <span data-ttu-id="2043a-211">Hello에 **Bamboo 사용자 계정** 섹션에서 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-211">On hello **Bamboo user accounts** section, perform following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    <span data-ttu-id="2043a-213">a.</span><span class="sxs-lookup"><span data-stu-id="2043a-213">a.</span></span> <span data-ttu-id="2043a-214">선택 **필요한 경우 Bamboo의 내부 디렉터리에서 사용자를 만들려면** 사용자에 대 한 hello 그룹의 hello 적절 한 이름을 입력 하 고 (수 여러 아니요.</span><span class="sxs-lookup"><span data-stu-id="2043a-214">Select **Create users in Bamboo's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="2043a-215">그룹의 쉼표로 구분).</span><span class="sxs-lookup"><span data-stu-id="2043a-215">of groups separated by comma).</span></span>

    <span data-ttu-id="2043a-216">b.</span><span class="sxs-lookup"><span data-stu-id="2043a-216">b.</span></span> <span data-ttu-id="2043a-217">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-217">Click **Next**.</span></span>

21. <span data-ttu-id="2043a-218">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-218">Click **Finish**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. <span data-ttu-id="2043a-220">Hello에 **도메인을 Azure AD에 대 한 알려진** 섹션에서 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-220">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

    <span data-ttu-id="2043a-222">a.</span><span class="sxs-lookup"><span data-stu-id="2043a-222">a.</span></span> <span data-ttu-id="2043a-223">선택 **알려진 도메인** hello hello 페이지의 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="2043a-223">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="2043a-224">b.</span><span class="sxs-lookup"><span data-stu-id="2043a-224">b.</span></span> <span data-ttu-id="2043a-225">Hello에 도메인 이름을 입력 **알려진 도메인** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-225">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="2043a-226">c.</span><span class="sxs-lookup"><span data-stu-id="2043a-226">c.</span></span> <span data-ttu-id="2043a-227">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-227">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2043a-228">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="2043a-228">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2043a-229">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="2043a-229">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2043a-230">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2043a-230">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2043a-231">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2043a-231">Creating an Azure AD test user</span></span>
<span data-ttu-id="2043a-232">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-232">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="2043a-234">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2043a-234">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2043a-235">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-235">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2043a-237">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-237">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2043a-239">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-239">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2043a-241">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-241">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2043a-243">a.</span><span class="sxs-lookup"><span data-stu-id="2043a-243">a.</span></span> <span data-ttu-id="2043a-244">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-244">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2043a-245">b.</span><span class="sxs-lookup"><span data-stu-id="2043a-245">b.</span></span> <span data-ttu-id="2043a-246">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-246">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2043a-247">c.</span><span class="sxs-lookup"><span data-stu-id="2043a-247">c.</span></span> <span data-ttu-id="2043a-248">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-248">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2043a-249">d.</span><span class="sxs-lookup"><span data-stu-id="2043a-249">d.</span></span> <span data-ttu-id="2043a-250">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-250">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a><span data-ttu-id="2043a-251">Kantega SSO for Bamboo 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2043a-251">Creating a Kantega SSO for Bamboo test user</span></span>

<span data-ttu-id="2043a-252">tooenable Azure AD 사용자가 toolog tooBamboo에서 이러한 해야에 프로 비전 Bamboo 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-252">tooenable Azure AD users toolog in tooBamboo, they must be provisioned into Bamboo.</span></span> <span data-ttu-id="2043a-253">Kantega SSO for Bamboo에서는 프로비전이 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-253">In Kantega SSO for Bamboo, provisioning is a manual task.</span></span>

<span data-ttu-id="2043a-254">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2043a-254">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2043a-255">Bamboo tooyour 프레미스 서버에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-255">Log in tooyour Bamboo on premise server as an administrator.</span></span>

2. <span data-ttu-id="2043a-256">Hello를 누르고 선 위에 마우스를 가져가면 **사용자 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-256">Hover on cog and click hello **User management**.</span></span>

    ![직원 추가](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. <span data-ttu-id="2043a-258">**사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-258">Click **Users**.</span></span> <span data-ttu-id="2043a-259">Hello에서 **사용자 추가** 섹션에서 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-259">Under hello **Add user** section, Perform follwing steps:</span></span>

    ![직원 추가](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    <span data-ttu-id="2043a-261">a.</span><span class="sxs-lookup"><span data-stu-id="2043a-261">a.</span></span> <span data-ttu-id="2043a-262">Hello에 **Username** 텍스트 형식 hello 전자 메일 사용자의 같은 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-262">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="2043a-263">b.</span><span class="sxs-lookup"><span data-stu-id="2043a-263">b.</span></span> <span data-ttu-id="2043a-264">Hello에 **암호** textbox, 사용자의 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-264">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="2043a-265">c.</span><span class="sxs-lookup"><span data-stu-id="2043a-265">c.</span></span> <span data-ttu-id="2043a-266">Hello에 **암호 확인** textbox, 사용자의 hello 암호 다시 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-266">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>
    
    <span data-ttu-id="2043a-267">d.</span><span class="sxs-lookup"><span data-stu-id="2043a-267">d.</span></span> <span data-ttu-id="2043a-268">Hello에 **전체 이름을** 텍스트 형식 Britta Simon 같은 hello 사용자의 전체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-268">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="2043a-269">e.</span><span class="sxs-lookup"><span data-stu-id="2043a-269">e.</span></span> <span data-ttu-id="2043a-270">Hello에 **전자 메일** textbox, 사용자의 hello 전자 메일 주소를 입력 같은 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-270">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="2043a-271">f.</span><span class="sxs-lookup"><span data-stu-id="2043a-271">f.</span></span> <span data-ttu-id="2043a-272">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-272">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2043a-273">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2043a-274">이 섹션에서는 액세스 tooKantega SSO Bamboo에 대 한 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Bamboo.</span></span>

![사용자 할당][200] 

<span data-ttu-id="2043a-276">**tooassign Britta Simon tooKantega Bamboo에 대 한 SSO hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2043a-276">**tooassign Britta Simon tooKantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="2043a-277">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2043a-279">Hello 응용 프로그램 목록에서 선택 **Bamboo에 대 한 SSO Kantega**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-279">In hello applications list, select **Kantega SSO for Bamboo**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. <span data-ttu-id="2043a-281">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="2043a-283">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-283">Click **Add** button.</span></span> <span data-ttu-id="2043a-284">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="2043a-286">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2043a-287">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2043a-288">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2043a-289">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2043a-289">Testing single sign-on</span></span>

<span data-ttu-id="2043a-290">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2043a-291">Hello 액세스 패널에에서 표시 하며 Bamboo 타일에 대 한 hello Kantega SSO를 클릭할 때 Bamboo 응용 프로그램에 대 한 자동으로 로그온 tooyour Kantega SSO를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-291">When you click hello Kantega SSO for Bamboo tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Bamboo application.</span></span>
<span data-ttu-id="2043a-292">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2043a-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2043a-293">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2043a-293">Additional resources</span></span>

* [<span data-ttu-id="2043a-294">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="2043a-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2043a-295">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2043a-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png


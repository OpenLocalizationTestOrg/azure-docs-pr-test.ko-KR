---
title: "자습서:Azure Active Directory와 Hosted Graphite 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 호스트 흑연색 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: d8914f6417ba8fbdef1a48e1b36635200ba130d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a><span data-ttu-id="70e03-103">자습서:Azure Active Directory와 Hosted Graphite 통합</span><span class="sxs-lookup"><span data-stu-id="70e03-103">Tutorial: Azure Active Directory integration with Hosted Graphite</span></span>

<span data-ttu-id="70e03-104">이 자습서에 설명 어떻게 toointegrate Hosted 흑연색 Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70e03-104">In this tutorial, you learn how toointegrate Hosted Graphite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70e03-105">호스트 흑연색 Azure AD와 통합 이점을 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="70e03-105">Integrating Hosted Graphite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70e03-106">액세스 tooHosted 흑연색을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-106">You can control in Azure AD who has access tooHosted Graphite</span></span>
- <span data-ttu-id="70e03-107">프로그램 사용자 tooautomatically get 로그온 tooHosted 흑연색 (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-107">You can enable your users tooautomatically get signed-on tooHosted Graphite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70e03-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="70e03-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70e03-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="70e03-110">Prerequisites</span></span>

<span data-ttu-id="70e03-111">흑연색 호스트와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-111">tooconfigure Azure AD integration with Hosted Graphite, you need hello following items:</span></span>

- <span data-ttu-id="70e03-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="70e03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70e03-113">Hosted Graphite Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="70e03-113">A Hosted Graphite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70e03-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70e03-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70e03-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="70e03-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70e03-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70e03-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="70e03-118">Scenario description</span></span>
<span data-ttu-id="70e03-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70e03-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70e03-121">Hello 갤러리에서 흑연색 호스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-121">Adding Hosted Graphite from hello gallery</span></span>
2. <span data-ttu-id="70e03-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="70e03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hosted-graphite-from-hello-gallery"></a><span data-ttu-id="70e03-123">Hello 갤러리에서 흑연색 호스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-123">Adding Hosted Graphite from hello gallery</span></span>
<span data-ttu-id="70e03-124">tooconfigure hello와의 통합 호스트 흑연색 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 호스팅 흑연색 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-124">tooconfigure hello integration of Hosted Graphite into Azure AD, you need tooadd Hosted Graphite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70e03-125">**hello 갤러리에서 Hosted 흑연색 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="70e03-125">**tooadd Hosted Graphite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e03-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70e03-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70e03-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="70e03-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="70e03-133">Hello 검색 상자에 입력 **호스팅된 흑연색**합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-133">In hello search box, type **Hosted Graphite**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. <span data-ttu-id="70e03-135">Hello 결과 패널에서 선택 **호스팅된 흑연색**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-135">In hello results panel, select **Hosted Graphite**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70e03-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="70e03-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70e03-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Hosted Graphite에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-138">In this section, you configure and test Azure AD single sign-on with Hosted Graphite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="70e03-139">Single sign on toowork에 대 한 Azure AD는 tooknow 흑연색 호스트에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hosted Graphite is tooa user in Azure AD.</span></span> <span data-ttu-id="70e03-140">즉, Azure AD 사용자 및 hello 흑연색 호스트의 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-140">In other words, a link relationship between an Azure AD user and hello related user in Hosted Graphite needs toobe established.</span></span>

<span data-ttu-id="70e03-141">호스트 흑연색에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-141">In Hosted Graphite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="70e03-142">tooconfigure 및 흑연색 호스트를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-142">tooconfigure and test Azure AD single sign-on with Hosted Graphite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70e03-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70e03-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70e03-145">**[호스팅된 흑연색 테스트 사용자 만들기](#creating-a-hosted-graphite-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 호스팅 흑연색에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-145">**[Creating a Hosted Graphite test user](#creating-a-hosted-graphite-test-user)** - toohave a counterpart of Britta Simon in Hosted Graphite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70e03-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70e03-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="70e03-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70e03-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="70e03-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70e03-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 흑연색 호스트 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hosted Graphite application.</span></span>

<span data-ttu-id="70e03-150">**Azure AD tooconfigure single sign on 흑연색 호스트와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="70e03-150">**tooconfigure Azure AD single sign-on with Hosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e03-151">Hello hello에 Azure 포털에서에서 **호스팅된 흑연색** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-151">In hello Azure portal, on hello **Hosted Graphite** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="70e03-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. <span data-ttu-id="70e03-155">Hello에 **호스팅된 흑연색 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP 시작 모드**, hello 다음 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="70e03-155">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    <span data-ttu-id="70e03-157">a.</span><span class="sxs-lookup"><span data-stu-id="70e03-157">a.</span></span> <span data-ttu-id="70e03-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://www.hostedgraphite.com/metadata/<user id>`</span><span class="sxs-lookup"><span data-stu-id="70e03-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/metadata/<user id>`</span></span>

    <span data-ttu-id="70e03-159">b.</span><span class="sxs-lookup"><span data-stu-id="70e03-159">b.</span></span> <span data-ttu-id="70e03-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://www.hostedgraphite.com/complete/saml/<user id>`</span><span class="sxs-lookup"><span data-stu-id="70e03-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/complete/saml/<user id>`</span></span>

4. <span data-ttu-id="70e03-161">Hello에 **호스팅된 흑연색 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **SP 시작 모드**, hello 다음 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="70e03-161">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    <span data-ttu-id="70e03-163">a.</span><span class="sxs-lookup"><span data-stu-id="70e03-163">a.</span></span> <span data-ttu-id="70e03-164">Hello 클릭 **고급 URL 설정 표시** 옵션</span><span class="sxs-lookup"><span data-stu-id="70e03-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="70e03-165">b.</span><span class="sxs-lookup"><span data-stu-id="70e03-165">b.</span></span> <span data-ttu-id="70e03-166">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://www.hostedgraphite.com/login/saml/<user id>/`</span><span class="sxs-lookup"><span data-stu-id="70e03-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/login/saml/<user id>/`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="70e03-167">이러한 없는지 hello 실제 값 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="70e03-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="70e03-168">Tooupdate hello로 이러한 값이 있는 실제 식별자, 회신 URL 및 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-168">You have tooupdate these values with hello actual Identifier, Reply URL and Sign On URL.</span></span> <span data-ttu-id="70e03-169">tooget 이들 값을 넘어가면 tooAccess 연락처 또는 응용 프로그램 쪽에서 SAML 설정-> [호스팅된 흑연색 지원 팀](mailto:help@hostedgraphite.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-169">tooget these values, you can go tooAccess->SAML setup on your Application side or Contact [Hosted Graphite support team](mailto:help@hostedgraphite.com).</span></span>
    >
 
5. <span data-ttu-id="70e03-170">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. <span data-ttu-id="70e03-172">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-172">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="70e03-174">Hello에 **호스팅 흑연색 구성을** 섹션에서 클릭 **호스팅된 흑연색 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="70e03-174">On hello **Hosted Graphite Configuration** section, click **Configure Hosted Graphite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="70e03-175">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="70e03-175">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. <span data-ttu-id="70e03-177">관리자 권한으로 로그온 tooyour 호스팅된 흑연색 테 넌 트.</span><span class="sxs-lookup"><span data-stu-id="70e03-177">Sign-on tooyour Hosted Graphite tenant as an administrator.</span></span>

9. <span data-ttu-id="70e03-178">Toohello 이동 **SAML 설치 페이지** hello 세로 막대에서 (**SAML 설정-> 액세스**).</span><span class="sxs-lookup"><span data-stu-id="70e03-178">Go toohello **SAML Setup page** in hello sidebar (**Access -> SAML Setup**).</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. <span data-ttu-id="70e03-180">이러한 Url 일치 hello에서 수행 하 여 구성을 확인 **호스팅된 흑연색 도메인 및 Url** hello Azure 포털의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-180">Confirm these URls match your configuration done on hello **Hosted Graphite Domain and URLs** section of hello Azure portal.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. <span data-ttu-id="70e03-182">**엔터티 또는 발급자 ID** 및 **SSO 로그인 URL** 입력란의 hello 값을 붙여넣습니다 **SAML 엔터티 ID** 및 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-182">In  **Entity or Issuer ID** and **SSO Login URL** textboxes, paste hello value of **SAML Entity ID** and **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. <span data-ttu-id="70e03-184">"**읽기 전용**"을 **기본 사용자 역할**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-184">Select "**Read-only**" as **Default User Role**.</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. <span data-ttu-id="70e03-186">콘텐츠를 클립보드에 복사 hello Azure 포털에서 다운로드 한 메모장에서 e-64로 인코딩된 인증서를 열고 toohello 붙여 **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. <span data-ttu-id="70e03-188">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="70e03-189">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="70e03-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="70e03-190">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="70e03-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="70e03-191">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70e03-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70e03-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="70e03-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="70e03-193">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="70e03-195">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="70e03-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e03-196">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70e03-198">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70e03-200">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70e03-202">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70e03-204">a.</span><span class="sxs-lookup"><span data-stu-id="70e03-204">a.</span></span> <span data-ttu-id="70e03-205">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70e03-206">b.</span><span class="sxs-lookup"><span data-stu-id="70e03-206">b.</span></span> <span data-ttu-id="70e03-207">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70e03-208">c.</span><span class="sxs-lookup"><span data-stu-id="70e03-208">c.</span></span> <span data-ttu-id="70e03-209">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="70e03-210">d.</span><span class="sxs-lookup"><span data-stu-id="70e03-210">d.</span></span> <span data-ttu-id="70e03-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-211">Click **Create**.</span></span>
 
### <a name="creating-a-hosted-graphite-test-user"></a><span data-ttu-id="70e03-212">Hosted Graphite 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="70e03-212">Creating a Hosted Graphite test user</span></span>

<span data-ttu-id="70e03-213">hello이이 섹션의 목적은 toocreate Britta Simon 흑연색 호스트에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-213">hello objective of this section is toocreate a user called Britta Simon in Hosted Graphite.</span></span> <span data-ttu-id="70e03-214">Hosted Graphite는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-214">Hosted Graphite supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="70e03-215">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-215">There is no action item for you in this section.</span></span> <span data-ttu-id="70e03-216">새 사용자를 아직 존재 하지 않는 경우 시도 tooaccess Hosted 흑연색 중 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-216">A new user will be created during an attempt tooaccess Hosted Graphite if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="70e03-217">Toocontact hello 호스트 흑연색 지원 팀을 통해 필요한 toocreate 사용자를 수동으로 해야 할 경우 < mailto:help@hostedgraphite.com >합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-217">If you need toocreate a user manually, you need toocontact hello Hosted Graphite support team via <mailto:help@hostedgraphite.com>.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="70e03-218">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="70e03-219">이 섹션에서는 액세스 tooHosted 흑연색 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHosted Graphite.</span></span>

![사용자 할당][200] 

<span data-ttu-id="70e03-221">**tooassign Britta Simon tooHosted 흑연색, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="70e03-221">**tooassign Britta Simon tooHosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="70e03-222">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="70e03-224">Hello 응용 프로그램 목록에서 선택 **호스팅된 흑연색**합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-224">In hello applications list, select **Hosted Graphite**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. <span data-ttu-id="70e03-226">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="70e03-228">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-228">Click **Add** button.</span></span> <span data-ttu-id="70e03-229">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="70e03-231">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70e03-232">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70e03-233">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70e03-234">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="70e03-234">Testing single sign-on</span></span>

<span data-ttu-id="70e03-235">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="70e03-236">Hello 액세스 패널에서에서 hello 호스트 흑연색 타일을 클릭할 때 자동으로 로그온 tooyour 흑연색 호스팅된 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70e03-236">When you click hello Hosted Graphite tile in hello Access Panel, you should get automatically signed-on tooyour Hosted Graphite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="70e03-237">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="70e03-237">Additional resources</span></span>

* [<span data-ttu-id="70e03-238">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="70e03-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70e03-239">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="70e03-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png


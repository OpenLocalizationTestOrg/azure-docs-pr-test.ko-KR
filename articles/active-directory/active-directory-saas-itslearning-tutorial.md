---
title: "자습서: itslearning과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 itslearning 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 60587ba3-1396-4b8a-9ac1-e22a98e5e0ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 4ee6c8d450cc3972a87da67fc79890473cfa498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itslearning"></a><span data-ttu-id="a3faf-103">자습서: itslearning과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a3faf-103">Tutorial: Azure Active Directory integration with itslearning</span></span>

<span data-ttu-id="a3faf-104">이 자습서에 설명 어떻게 toointegrate itslearning Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a3faf-104">In this tutorial, you learn how toointegrate itslearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3faf-105">다음 이점을 hello로 제공 itslearning Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="a3faf-105">Integrating itslearning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a3faf-106">액세스 tooitslearning을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-106">You can control in Azure AD who has access tooitslearning</span></span>
- <span data-ttu-id="a3faf-107">프로그램 사용자 tooautomatically get 로그온 tooitslearning (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-107">You can enable your users tooautomatically get signed-on tooitslearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a3faf-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a3faf-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3faf-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a3faf-110">Prerequisites</span></span>

<span data-ttu-id="a3faf-111">다음 항목 hello가 필요 tooconfigure itslearning와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-111">tooconfigure Azure AD integration with itslearning, you need hello following items:</span></span>

- <span data-ttu-id="a3faf-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a3faf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a3faf-113">Itslearning Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a3faf-113">An itslearning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3faf-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3faf-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3faf-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a3faf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a3faf-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3faf-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a3faf-118">Scenario description</span></span>
<span data-ttu-id="a3faf-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a3faf-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3faf-121">Itslearning hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="a3faf-121">Adding itslearning from hello gallery</span></span>
2. <span data-ttu-id="a3faf-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a3faf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itslearning-from-hello-gallery"></a><span data-ttu-id="a3faf-123">Itslearning hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="a3faf-123">Adding itslearning from hello gallery</span></span>
<span data-ttu-id="a3faf-124">tooconfigure hello와의 통합 itslearning Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd itslearning이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-124">tooconfigure hello integration of itslearning into Azure AD, you need tooadd itslearning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a3faf-125">**hello 갤러리에서 tooadd itslearning hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a3faf-125">**tooadd itslearning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3faf-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a3faf-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a3faf-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a3faf-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a3faf-133">Hello 검색 상자에 입력 **itslearning**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-133">In hello search box, type **itslearning**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_search.png)

5. <span data-ttu-id="a3faf-135">Hello 결과 패널에서 선택 **itslearning**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-135">In hello results panel, select **itslearning**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a3faf-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a3faf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a3faf-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 itslearning에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-138">In this section, you configure and test Azure AD single sign-on with itslearning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a3faf-139">Single sign on toowork에 대 한 Azure AD는 tooknow itslearning에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in itslearning is tooa user in Azure AD.</span></span> <span data-ttu-id="a3faf-140">즉, Azure AD 사용자 및 itslearning에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-140">In other words, a link relationship between an Azure AD user and hello related user in itslearning needs toobe established.</span></span>

<span data-ttu-id="a3faf-141">Itslearning에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-141">In itslearning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a3faf-142">tooconfigure 및 itslearning 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-142">tooconfigure and test Azure AD single sign-on with itslearning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a3faf-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a3faf-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a3faf-145">**[Itslearning 테스트 사용자 만들기](#creating-an-itslearning-test-user)**  -toohave에서 사용자의 연결 된 Azure AD toohello 표현인 itslearning Britta Simon 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-145">**[Creating an itslearning test user](#creating-an-itslearning-test-user)** - toohave a counterpart of Britta Simon in itslearning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a3faf-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a3faf-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="a3faf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a3faf-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a3faf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a3faf-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 itslearning 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your itslearning application.</span></span>

<span data-ttu-id="a3faf-150">**tooconfigure Azure AD single sign on, itslearning와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a3faf-150">**tooconfigure Azure AD single sign-on with itslearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3faf-151">Hello hello에 Azure 포털에서에서 **itslearning** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-151">In hello Azure portal, on hello **itslearning** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a3faf-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_samlbase.png)

3. <span data-ttu-id="a3faf-155">Hello에 **itslearning 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-155">On hello **itslearning Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_url.png)

    <span data-ttu-id="a3faf-157">a.</span><span class="sxs-lookup"><span data-stu-id="a3faf-157">a.</span></span> <span data-ttu-id="a3faf-158">Hello에 **로그온 URL** 텍스트 상자에 다음 URL로:</span><span class="sxs-lookup"><span data-stu-id="a3faf-158">In hello **Sign-on URL** textbox, type a URL as:</span></span>
    | |
    |--| 
    | `https://www.itslearning.com/index.aspx`|
    | `https://us1.itslearning.com/index.aspx`|

    <span data-ttu-id="a3faf-159">b.</span><span class="sxs-lookup"><span data-stu-id="a3faf-159">b.</span></span> <span data-ttu-id="a3faf-160">Hello에 **식별자** 텍스트 상자에 다음 URL로:`urn:mace:saml2v2.no:services:com.itslearning`</span><span class="sxs-lookup"><span data-stu-id="a3faf-160">In hello **Identifier** textbox, type a URL as: `urn:mace:saml2v2.no:services:com.itslearning`</span></span>

4. <span data-ttu-id="a3faf-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_certificate.png) 

5. <span data-ttu-id="a3faf-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-itslearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a3faf-165">tooconfigure single sign on에서 **itslearning** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[itslearning 지원 팀](mailto:support@itslearning.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-165">tooconfigure single sign-on on **itslearning** side, you need toosend hello downloaded **Metadata XML** too[itslearning support team](mailto:support@itslearning.com).</span></span> <span data-ttu-id="a3faf-166">이 설정은 toohave hello 양쪽 모두에 제대로 설정 하는 SAML SSO 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a3faf-167">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="a3faf-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a3faf-168">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="a3faf-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a3faf-169">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a3faf-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a3faf-170">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a3faf-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="a3faf-171">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a3faf-173">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a3faf-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3faf-174">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itslearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a3faf-176">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itslearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a3faf-178">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itslearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a3faf-180">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-itslearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a3faf-182">a.</span><span class="sxs-lookup"><span data-stu-id="a3faf-182">a.</span></span> <span data-ttu-id="a3faf-183">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a3faf-184">b.</span><span class="sxs-lookup"><span data-stu-id="a3faf-184">b.</span></span> <span data-ttu-id="a3faf-185">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a3faf-186">c.</span><span class="sxs-lookup"><span data-stu-id="a3faf-186">c.</span></span> <span data-ttu-id="a3faf-187">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a3faf-188">d.</span><span class="sxs-lookup"><span data-stu-id="a3faf-188">d.</span></span> <span data-ttu-id="a3faf-189">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-189">Click **Create**.</span></span>
 
### <a name="creating-an-itslearning-test-user"></a><span data-ttu-id="a3faf-190">Itslearning 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a3faf-190">Creating an itslearning test user</span></span>

<span data-ttu-id="a3faf-191">이 섹션에서는 itslearning에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-191">In this section, you create a user called Britta Simon in itslearning.</span></span> <span data-ttu-id="a3faf-192">작업할 [itslearning 클라이언트 지원 팀](mailto:support@itslearning.com) hello 사용자 hello itslearning 플랫폼을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-192">Work with [itslearning Client support team](mailto:support@itslearning.com) to add hello users in hello itslearning platform.</span></span> <span data-ttu-id="a3faf-193">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a3faf-194">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a3faf-195">이 섹션에서는 tooitslearning 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooitslearning.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a3faf-197">**tooassign Britta Simon tooitslearning hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a3faf-197">**tooassign Britta Simon tooitslearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3faf-198">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a3faf-200">Hello 응용 프로그램 목록에서 선택 **itslearning**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-200">In hello applications list, select **itslearning**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_app.png) 

3. <span data-ttu-id="a3faf-202">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a3faf-204">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-204">Click **Add** button.</span></span> <span data-ttu-id="a3faf-205">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a3faf-207">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a3faf-208">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a3faf-209">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a3faf-210">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a3faf-210">Testing single sign-on</span></span>

<span data-ttu-id="a3faf-211">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a3faf-212">Hello 액세스 패널에서에서 hello itslearning 타일을 클릭할 때 itslearning 응용 프로그램의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-212">When you click hello itslearning tile in hello Access Panel, you should get login page of itslearning application.</span></span> <span data-ttu-id="a3faf-213">클릭 **Windows Azure ACS1 로그인** hello 응용 프로그램에 성공적으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-213">Click **Log in with Windows Azure ACS1** for successful login into hello application.</span></span>

  ![로그인](./media/active-directory-saas-itslearning-tutorial/login.png)

<span data-ttu-id="a3faf-215">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3faf-215">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a3faf-216">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a3faf-216">Additional resources</span></span>

* [<span data-ttu-id="a3faf-217">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="a3faf-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3faf-218">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a3faf-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_203.png


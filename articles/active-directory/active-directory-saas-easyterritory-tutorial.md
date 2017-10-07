---
title: "자습서: EasyTerritory와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 EasyTerritory 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4f1e9fb4d615325f0d57bebaed955529d5dcd9b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="6d192-103">자습서: EasyTerritory와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="6d192-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="6d192-104">이 자습서에 설명 어떻게 toointegrate EasyTerritory Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d192-104">In this tutorial, you learn how toointegrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d192-105">다음 이점을 hello로 제공 EasyTerritory Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="6d192-105">Integrating EasyTerritory with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6d192-106">액세스 tooEasyTerritory을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-106">You can control in Azure AD who has access tooEasyTerritory.</span></span>
- <span data-ttu-id="6d192-107">에 사용자가 tooautomatically get 로그온 tooEasyTerritory (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-107">You can enable your users tooautomatically get signed-on tooEasyTerritory (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6d192-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6d192-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d192-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6d192-110">Prerequisites</span></span>

<span data-ttu-id="6d192-111">다음 항목 hello가 필요 tooconfigure EasyTerritory와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-111">tooconfigure Azure AD integration with EasyTerritory, you need hello following items:</span></span>

- <span data-ttu-id="6d192-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="6d192-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d192-113">EasyTerritory Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="6d192-113">A EasyTerritory single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6d192-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d192-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d192-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6d192-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d192-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d192-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="6d192-118">Scenario description</span></span>
<span data-ttu-id="6d192-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d192-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d192-121">EasyTerritory는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="6d192-121">Adding EasyTerritory from hello gallery</span></span>
2. <span data-ttu-id="6d192-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6d192-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-easyterritory-from-hello-gallery"></a><span data-ttu-id="6d192-123">EasyTerritory는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="6d192-123">Adding EasyTerritory from hello gallery</span></span>
<span data-ttu-id="6d192-124">tooconfigure hello와의 통합 EasyTerritory Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 EasyTerritory tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-124">tooconfigure hello integration of EasyTerritory into Azure AD, you need tooadd EasyTerritory from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6d192-125">**hello 갤러리에서 EasyTerritory tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6d192-125">**tooadd EasyTerritory from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d192-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="6d192-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6d192-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="6d192-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="6d192-133">Hello 검색 상자에 입력 **EasyTerritory**선택, **EasyTerritory** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-133">In hello search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button tooadd hello application.</span></span>

    ![EasyTerritory hello 결과 목록에서](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6d192-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6d192-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6d192-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 EasyTerritory에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6d192-137">Single sign on toowork에 대 한 Azure AD는 tooknow EasyTerritory에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EasyTerritory is tooa user in Azure AD.</span></span> <span data-ttu-id="6d192-138">즉, Azure AD 사용자 및 EasyTerritory에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-138">In other words, a link relationship between an Azure AD user and hello related user in EasyTerritory needs toobe established.</span></span>

<span data-ttu-id="6d192-139">EasyTerritory에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-139">In EasyTerritory, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6d192-140">tooconfigure 및 EasyTerritory 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-140">tooconfigure and test Azure AD single sign-on with EasyTerritory, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6d192-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6d192-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d192-143">**[EasyTerritory 테스트 사용자 만들기](#create-a-easyterritory-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 EasyTerritory에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - toohave a counterpart of Britta Simon in EasyTerritory that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6d192-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d192-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="6d192-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6d192-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="6d192-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6d192-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 EasyTerritory 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EasyTerritory application.</span></span>

<span data-ttu-id="6d192-148">**tooconfigure Azure AD single sign on, EasyTerritory와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6d192-148">**tooconfigure Azure AD single sign-on with EasyTerritory, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d192-149">Hello hello에 Azure 포털에서에서 **EasyTerritory** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-149">In hello Azure portal, on hello **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="6d192-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_samlbase.png)

3. <span data-ttu-id="6d192-153">Hello에 **EasyTerritory 도메인 및 Url** 섹션를 hello IDP의 tooconfigure hello 응용 프로그램 시작 모드를 원하는 경우 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-153">On hello **EasyTerritory Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![EasyTerritory 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url.png)

    <span data-ttu-id="6d192-155">a.</span><span class="sxs-lookup"><span data-stu-id="6d192-155">a.</span></span> <span data-ttu-id="6d192-156">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://apps.easyterritory.com/<tenant id>/dev/`</span><span class="sxs-lookup"><span data-stu-id="6d192-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span></span>

    <span data-ttu-id="6d192-157">b.</span><span class="sxs-lookup"><span data-stu-id="6d192-157">b.</span></span> <span data-ttu-id="6d192-158">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span><span class="sxs-lookup"><span data-stu-id="6d192-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span></span>

4. <span data-ttu-id="6d192-159">확인 **고급 URL 설정 표시** hello tooconfigure hello 응용 프로그램에 필요한 경우 단계를 다음을 수행 하 고 **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="6d192-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![EasyTerritory 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url1.png)

    <span data-ttu-id="6d192-161">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.easyterritory.com/`</span><span class="sxs-lookup"><span data-stu-id="6d192-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.easyterritory.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="6d192-162">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-162">These values are not real.</span></span> <span data-ttu-id="6d192-163">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="6d192-164">연락처 [EasyTerritory 클라이언트 지원 팀](mailto:sales@easyterritory.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) tooget these values.</span></span> 

5. <span data-ttu-id="6d192-165">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_certificate.png) 

6. <span data-ttu-id="6d192-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-167">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6d192-169">tooconfigure single sign on에서 **EasyTerritory** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[EasyTerritory 지원 팀](mailto:sales@easyterritory.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-169">tooconfigure single sign-on on **EasyTerritory** side, you need toosend hello downloaded **Metadata XML** too[EasyTerritory support team](mailto:sales@easyterritory.com).</span></span> <span data-ttu-id="6d192-170">이 설정은 toohave hello 양쪽 모두에 제대로 설정 하는 SAML SSO 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6d192-171">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="6d192-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6d192-172">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="6d192-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6d192-173">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6d192-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6d192-174">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6d192-174">Create an Azure AD test user</span></span>

<span data-ttu-id="6d192-175">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="6d192-177">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6d192-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d192-178">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6d192-180">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6d192-182">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="6d192-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6d192-184">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6d192-186">a.</span><span class="sxs-lookup"><span data-stu-id="6d192-186">a.</span></span> <span data-ttu-id="6d192-187">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d192-188">b.</span><span class="sxs-lookup"><span data-stu-id="6d192-188">b.</span></span> <span data-ttu-id="6d192-189">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6d192-190">c.</span><span class="sxs-lookup"><span data-stu-id="6d192-190">c.</span></span> <span data-ttu-id="6d192-191">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6d192-192">d.</span><span class="sxs-lookup"><span data-stu-id="6d192-192">d.</span></span> <span data-ttu-id="6d192-193">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-193">Click **Create**.</span></span>
 
### <a name="create-a-easyterritory-test-user"></a><span data-ttu-id="6d192-194">EasyTerritory 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6d192-194">Create a EasyTerritory test user</span></span>

<span data-ttu-id="6d192-195">이 섹션에서는 EasyTerritory에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-195">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="6d192-196">와 협력 하세요 [EasyTerritory 지원 팀](mailto:sales@easyterritory.com) hello EasyTerritory 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) tooadd hello users in hello EasyTerritory platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6d192-197">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6d192-198">이 섹션에서는 tooEasyTerritory 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEasyTerritory.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="6d192-200">**tooassign Britta Simon tooEasyTerritory hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6d192-200">**tooassign Britta Simon tooEasyTerritory, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d192-201">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="6d192-203">Hello 응용 프로그램 목록에서 선택 **EasyTerritory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-203">In hello applications list, select **EasyTerritory**.</span></span>

    ![hello 응용 프로그램 목록에서 hello EasyTerritory 링크](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_app.png)  

3. <span data-ttu-id="6d192-205">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="6d192-207">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-207">Click **Add** button.</span></span> <span data-ttu-id="6d192-208">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="6d192-210">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6d192-211">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d192-212">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6d192-213">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="6d192-213">Test single sign-on</span></span>

<span data-ttu-id="6d192-214">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6d192-215">Hello 액세스 패널에서에서 hello EasyTerritory 타일을 클릭할 때 자동으로 로그온 tooyour EasyTerritory 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-215">When you click hello EasyTerritory tile in hello Access Panel, you should get automatically signed-on tooyour EasyTerritory application.</span></span>
<span data-ttu-id="6d192-216">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d192-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6d192-217">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6d192-217">Additional resources</span></span>

* [<span data-ttu-id="6d192-218">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="6d192-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d192-219">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6d192-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)




<!--Image references-->

[1]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png


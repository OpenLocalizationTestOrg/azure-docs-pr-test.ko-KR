---
title: "자습서: Help Scout와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 도움말 Scout 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="d26e4-103">자습서: Help Scout와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d26e4-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="d26e4-104">이 자습서에서는 toointegrate 도움말 Azure Active Directory (Azure AD)와 정찰 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-104">In this tutorial, you learn how toointegrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d26e4-105">도움말 Scout를 Azure AD와 통합에서 혜택을 따라 hello를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-105">You get hello following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="d26e4-106">Azure AD에서 액세스 tooHelp Scout를가지고 있는 사람을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-106">In Azure AD, you can control who has access tooHelp Scout.</span></span>
- <span data-ttu-id="d26e4-107">Single sign on 및 사용자의 Azure AD 계정을 사용 하 여 사용자가 tooHelp Scout 프로그램에 자동으로 서명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-107">You can automatically sign in your users tooHelp Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="d26e4-108">프로그램을 하나의 중앙 위치에 hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="d26e4-109">참조로 Azure AD와 saas () 응용 프로그램 통합 소프트웨어에 대해 자세히 toolearn [응용 프로그램 액세스 및 single sign on Azure Active directory 란?](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d26e4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d26e4-110">Prerequisites</span></span>

<span data-ttu-id="d26e4-111">Azure AD와 통합 된 도움말 Scout을 tooset, 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-111">tooset up Azure AD integration with Help Scout, you need hello following items:</span></span>

- <span data-ttu-id="d26e4-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d26e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d26e4-113">Single Sign-On이 설정된 Help Scout 구독</span><span class="sxs-lookup"><span data-stu-id="d26e4-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="d26e4-114">이 자습서에서는 hello 단계를 테스트 하는 경우는 프로덕션 환경에서 테스트할 하지 있습니다 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="d26e4-115">이 자습서에서는 hello 단계를 테스트 하기 위한 권장 사항:</span><span class="sxs-lookup"><span data-stu-id="d26e4-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="d26e4-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d26e4-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="d26e4-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d26e4-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d26e4-118">Scenario description</span></span>
<span data-ttu-id="d26e4-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="d26e4-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d26e4-121">Hello 갤러리에서 Scout 도움말을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-121">Add Help Scout from hello gallery.</span></span>
2. <span data-ttu-id="d26e4-122">Azure AD Single Sign-On 설정 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d26e4-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-hello-gallery"></a><span data-ttu-id="d26e4-123">도움말 Scout hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="d26e4-123">Add Help Scout from hello gallery</span></span>
<span data-ttu-id="d26e4-124">hello와 도움말 Scout hello 갤러리에서 Azure AD와의 통합을 tooset 도움말 Scout tooyour 목록은 관리 되는 SaaS 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-124">tooset up hello integration of Help Scout with Azure AD, in hello gallery, add Help Scout tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d26e4-125">tooadd hello 갤러리에서 Scout 도움말:</span><span class="sxs-lookup"><span data-stu-id="d26e4-125">tooadd Help Scout from hello gallery:</span></span>

1. <span data-ttu-id="d26e4-126">Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 메뉴에서 선택 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="d26e4-128">**엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 페이지][2]
    
3. <span data-ttu-id="d26e4-130">새 응용 프로그램을 tooadd 선택 **새 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-130">tooadd a new application, select **New application**.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="d26e4-132">Hello 검색 상자에 입력 **도움말 Scout**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-132">In hello search box, enter **Help Scout**.</span></span> <span data-ttu-id="d26e4-133">Hello 검색 결과에서 선택 **도움말 Scout**를 선택한 후 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-133">In hello search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Hello 결과 목록에서 Scout 도움말](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d26e4-135">Azure AD Single Sign-On 설정 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d26e4-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="d26e4-136">이 섹션에서는 *Britta Simon*이라는 테스트 사용자를 기반으로 Help Scout에서 Azure AD Single Sign-On을 설정하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="d26e4-137">Azure AD single sign on toowork에 대 한 도움말 Scout tooknow hello Azure AD에 관련 사용자는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-137">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="d26e4-138">Azure AD 사용자 및 도움말 Scout에 hello 관련된 사용자 간 링크 관계를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-138">A link relationship between an Azure AD user and hello related user in Help Scout must be established.</span></span>

<span data-ttu-id="d26e4-139">tooestablish hello에 대 한 관계에 Scout 도움말 링크 **Username**, hello hello 값을 할당 **사용자 이름** Azure AD에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-139">tooestablish hello link relationship, in Help Scout, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="d26e4-140">tooconfigure 및 도움말 정찰, 작업을 수행 하는 전체 hello 사용 하 여 Azure AD에서 single sign-on 테스트:</span><span class="sxs-lookup"><span data-stu-id="d26e4-140">tooconfigure and test Azure AD single sign-on with Help Scout, complete hello following tasks:</span></span>

1. <span data-ttu-id="d26e4-141">[Azure AD Single Sign-On 설정](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d26e4-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="d26e4-142">이 기능은 사용자 toouse를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-142">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="d26e4-143">[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="d26e4-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="d26e4-144">테스트 Azure AD single sign on hello 사용자 Britta Simon와 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-144">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="d26e4-145">[Help Scout 테스트 사용자 만들기](#create-a-help-scout-test-user)</span><span class="sxs-lookup"><span data-stu-id="d26e4-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="d26e4-146">연결 된 toohello hello 사용자의 Azure AD 표현 되는 데 도움이 Scout에 Britta Simon의 해당 하는 도구를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-146">Creates a counterpart of Britta Simon in Help Scout that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="d26e4-147">[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-147">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="d26e4-148">Azure AD에서 single sign-on Britta Simon toouse를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-148">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d26e4-149">[Single Sign-On 테스트](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d26e4-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="d26e4-150">해당 hello 구성이 작동을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-150">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="d26e4-151">Azure AD Single Sign-On 설정</span><span class="sxs-lookup"><span data-stu-id="d26e4-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="d26e4-152">이 섹션에서는 Azure AD single sign-on을 hello Azure 포털에서에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-152">In this section, you set up Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="d26e4-153">그런 다음 Help Scout 응용 프로그램에서 Single Sign-On을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="d26e4-154">Azure AD single sign-on을 도움말 Scout와 tooset:</span><span class="sxs-lookup"><span data-stu-id="d26e4-154">tooset up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="d26e4-155">Hello hello에 Azure 포털에서에서 **도움말 Scout** 응용 프로그램 통합 페이지에서 선택 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-155">In hello Azure portal, on hello **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Single Sign-On 설정 링크][4]

2. <span data-ttu-id="d26e4-157">Hello에 **Single sign on** 페이지에 대 한 **모드**선택, **SAML 기반 로그온**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-157">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="d26e4-159">아래 **도움말 Scout 도메인 및 Url**IDP 시작 모드에서는 단계를 수행 하는 전체 hello tooset hello 응용 프로그램을 설치 하려는 경우:</span><span class="sxs-lookup"><span data-stu-id="d26e4-159">Under **Help Scout Domain and URLs**, if you want tooset up hello application in IDP-initiated mode, complete hello following steps:</span></span>

    1. <span data-ttu-id="d26e4-160">Hello에 **식별자** 상자에 URL hello 패턴을 입력 합니다.`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="d26e4-160">In hello **Identifier** box, enter a URL that has hello following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="d26e4-161">Hello에 **회신 URL** 상자에 URL hello 패턴을 입력 합니다.`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="d26e4-161">In hello **Reply URL** box, enter a URL that has hello following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Help Scout 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="d26e4-163">SP에서 시작한 모드로 tooset hello 응용 프로그램을 설치 하려는 경우 선택 hello **고급 URL 설정 표시** 확인란을 선택한 수행가 다음를 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="d26e4-163">If you want tooset up hello application in SP-initiated mode, select hello **Show advanced URL settings** check box, and then do hello following:</span></span>

    * <span data-ttu-id="d26e4-164">Hello에 **로그온 URL** 상자 형식에 따라 hello에 하는 URL을 입력 합니다.`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="d26e4-164">In hello **Sign on URL** box, enter a URL that has hello following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Help Scout 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="d26e4-166">이러한 Url hello 값 데모 목적 으로만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-166">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="d26e4-167">Hello 실제 식별자 URL 및 회신 URL hello 값으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-167">Update hello values with hello actual identifier URL and reply URL.</span></span> <span data-ttu-id="d26e4-168">이러한 값에 게 문의 tooget [Scout 도움말 지원 팀](mailto:help@helpscout.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-168">tooget these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="d26e4-169">아래 **SAML 서명 인증서**선택, **메타 데이터 XML**, hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="d26e4-171">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-171">Select **Save**.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="d26e4-173">단일을 tooset 로그온 hello 도움말 Scout 쪽, 송신 hello 다운로드 한 메타 데이터 XML 파일 toohello [Scout 도움말 지원 팀](mailto:help@helpscout.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-173">tooset up single sign-on on hello Help Scout side, send hello downloaded metadata XML file toohello [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="d26e4-174">hello Scout 도움말 지원 팀 hello SAML single sign on 연결 양쪽 모두 올바르게 설정 되도록이 설정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-174">hello Help Scout support team applies this setting so that hello SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d26e4-175">Hello에이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)응용 프로그램을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="d26e4-175">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="d26e4-176">선택 하 여 hello 앱을 추가한 후 **Active Directory** > **엔터프라이즈 응용 프로그램**선택, hello **Single Sign On** 탭 합니다. Hello에 포함 된 hello 설명서에 액세스할 수 있습니다 **구성** 섹션 hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-176">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="d26e4-177">자세한 내용은 [Azure AD 포함 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d26e4-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d26e4-178">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d26e4-178">Create an Azure AD test user</span></span>

<span data-ttu-id="d26e4-179">Hello Azure 포털에서에서이 섹션에서는 Britta Simon 이라는 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-179">In this section, in hello Azure portal, you create a test user named Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="d26e4-181">Azure AD에서 테스트 사용자 toocreate:</span><span class="sxs-lookup"><span data-stu-id="d26e4-181">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="d26e4-182">Hello hello 왼쪽된 메뉴에 Azure 포털에서에서 선택 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-182">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d26e4-184">사용자 선택 toodisplay hello 목록 **사용자 및 그룹**, 선택한 후 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-184">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![사용자 및 그룹 선택 및 모든 사용자 선택](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d26e4-186">tooopen hello **사용자** hello 위쪽 hello에 대화 상자에서 **모든 사용자에 게** 페이지에서 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-186">tooopen hello **User** dialog box, at hello top of hello **All Users** page, select **Add**.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d26e4-188">Hello에 **사용자** 대화 상자에서 다음 단계 완료 hello:</span><span class="sxs-lookup"><span data-stu-id="d26e4-188">In hello **User** dialog box, complete hello following steps:</span></span>

    1. <span data-ttu-id="d26e4-189">Hello에 **이름** 상자에 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-189">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="d26e4-190">Hello에 **사용자 이름** 상자에 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-190">In hello **User name** box, enter hello email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="d26e4-191">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="d26e4-192">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-192">Select **Create**.</span></span>

        ![hello 사용자 대화 상자](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="d26e4-194">Help Scout 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d26e4-194">Create a Help Scout test user</span></span>

<span data-ttu-id="d26e4-195">이 섹션의 hello 목표 toocreate Britta Simon Scout 도움말의 라는 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-195">hello object of this section is toocreate a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="d26e4-196">Help Scout는 JIT(Just-In-Time) 프로비전을 지원하며 이 기능은 기본적으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="d26e4-197">이 섹션에는 액션 또는 작업 toocomplete 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-197">In this section, there's no action or task toocomplete.</span></span> <span data-ttu-id="d26e4-198">사용자 도움말 Scout에 존재 하지 않으면 새 tooaccess Scout 도움말을 시도할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt tooaccess Help Scout.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d26e4-199">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d26e4-200">이 섹션에서는 hello 사용자 계정 액세스 tooHelp Scout 권한을 부여 하 여 toouse Azure AD에서 single sign-on hello 사용자 Britta Simon를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-200">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooHelp Scout.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="d26e4-202">tooassign Britta Simon tooHelp Scout:</span><span class="sxs-lookup"><span data-stu-id="d26e4-202">tooassign Britta Simon tooHelp Scout:</span></span>

1. <span data-ttu-id="d26e4-203">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 고 toohello 디렉터리 보기를 이동 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d26e4-203">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="d26e4-204">**엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d26e4-206">Hello 응용 프로그램 목록에서 선택 **도움말 Scout**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-206">In hello applications list, select **Help Scout**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Scout 도움말 링크](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="d26e4-208">Hello 왼쪽된 메뉴에서 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-208">In hello left menu, select **Users and groups**.</span></span>

    ![hello 사용자 및 그룹 링크][202]

4. <span data-ttu-id="d26e4-210">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-210">Select **Add**.</span></span> <span data-ttu-id="d26e4-211">그런 다음 hello **할당 추가** 페이지에서 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-211">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="d26e4-213">Hello에 **사용자 및 그룹** 페이지의 사용자를 hello 목록 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-213">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="d26e4-214">Hello에 **사용자 및 그룹** 페이지에서 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-214">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="d26e4-215">Hello에 **할당 추가** 페이지에서 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-215">On hello **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d26e4-216">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d26e4-216">Test single sign-on</span></span>

<span data-ttu-id="d26e4-217">이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD single sign on 구성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-217">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="d26e4-218">Hello 액세스 패널에서 hello 도움말 Scout 타일을 선택 하면 해야 자동으로 로그인 됩니다 tooyour 도움말 Scout 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-218">When you select hello Help Scout tile in hello access panel, you should be automatically signed in tooyour Help Scout application.</span></span>

<span data-ttu-id="d26e4-219">액세스 패널에 대 한 자세한 내용은 참조 [toohello 액세스 패널 소개](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d26e4-219">For more information about the access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d26e4-220">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d26e4-220">Additional resources</span></span>

* [<span data-ttu-id="d26e4-221">방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="d26e4-221">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d26e4-222">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d26e4-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png


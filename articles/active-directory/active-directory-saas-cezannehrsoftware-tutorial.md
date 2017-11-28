---
title: "자습서: Cezanne HR 소프트웨어와 Azure Active Directory 통합| Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Cezanne HR 소프트웨어 간의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="ecb80-103">자습서: Cezanne HR 소프트웨어와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="ecb80-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="ecb80-104">이 자습서에 설명 어떻게 toointegrate Cezanne HR 소프트웨어와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ecb80-104">In this tutorial, you learn how toointegrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ecb80-105">Cezanne HR 소프트웨어 Azure AD와 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-105">Integrating Cezanne HR software with Azure AD provides you with hello following benefits.</span></span> <span data-ttu-id="ecb80-106">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-106">You can:</span></span>

- <span data-ttu-id="ecb80-107">HR 소프트웨어 액세스 tooCezanne을 지닌 Azure AD에서 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-107">Control in Azure AD who has access tooCezanne HR software.</span></span>
- <span data-ttu-id="ecb80-108">Single sign-on에서 SSO ()는 Azure AD 계정을 사용 tooCezanne HR 소프트웨어에 대 한 사용자가 tooautomatically 로그인을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-108">Enable your users tooautomatically sign in tooCezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ecb80-109">하나의 중앙 위치에 계정 관리: hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="ecb80-110">로 Azure AD와 saas () 응용 프로그램 통합 소프트웨어에 대해 자세히 toolearn 참조 [응용 프로그램 액세스 및 SSO 및 Azure Active Directory 란?](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-110">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecb80-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ecb80-111">Prerequisites</span></span>

<span data-ttu-id="ecb80-112">다음 항목 hello가 필요 tooconfigure Cezanne HR software와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-112">tooconfigure Azure AD integration with Cezanne HR software, you need hello following items:</span></span>

- <span data-ttu-id="ecb80-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="ecb80-113">An Azure AD subscription</span></span>
- <span data-ttu-id="ecb80-114">Cezanne HR 소프트웨어 SSO가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="ecb80-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ecb80-115">이 자습서의 tootest hello 단계, 프로덕션 환경 사용 하지 않으면 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-115">tootest hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="ecb80-116">이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="ecb80-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="ecb80-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ecb80-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ecb80-118">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ecb80-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="ecb80-119">Scenario description</span></span>
<span data-ttu-id="ecb80-120">이 자습서에서는 테스트 환경에서 Azure AD SSO를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="ecb80-121">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="ecb80-122">Hello 갤러리에서 Cezanne HR 소프트웨어 추가</span><span class="sxs-lookup"><span data-stu-id="ecb80-122">Adding Cezanne HR software from hello gallery</span></span>
* <span data-ttu-id="ecb80-123">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ecb80-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-hello-gallery"></a><span data-ttu-id="ecb80-124">Hello 갤러리에서 Cezanne HR 소프트웨어를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-124">Add Cezanne HR software from hello gallery</span></span>
<span data-ttu-id="ecb80-125">tooconfigure hello 통합 Cezanne HR 소프트웨어의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Cezanne HR 소프트웨어를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-125">tooconfigure hello integration of Cezanne HR software into Azure AD, add Cezanne HR software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ecb80-126">tooadd hello 갤러리에서 Cezanne HR 소프트웨어 않으면 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="ecb80-126">tooadd Cezanne HR software from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="ecb80-127">Hello에 ** [Azure 포털](https://portal.azure.com)**hello 왼쪽된 창에서 선택 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-127">In hello **[Azure portal](https://portal.azure.com)**, in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![hello "Azure Active Directory" 단추][1]

2. <span data-ttu-id="ecb80-129">**엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-129">Select **Enterprise applications** > **All applications**.</span></span>

    !["모든 응용 프로그램" 링크를 hello][2]
    
3. <span data-ttu-id="ecb80-131">tooadd hello hello 위쪽에 새 응용 프로그램 **모든 응용 프로그램** 대화 상자에서 **새 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-131">tooadd a new application, at hello top of hello **All applications** dialog box, select **New application**.</span></span>

    !["새 응용 프로그램" hello 단추][3]

4. <span data-ttu-id="ecb80-133">Hello 검색 상자에 입력 **Cezanne HR 소프트웨어**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-133">In hello search box, type **Cezanne HR Software**.</span></span>

    ![hello 검색 상자](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="ecb80-135">Hello 결과 목록에서 선택 **Cezanne HR 소프트웨어** 선택한 후 hello **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-135">In hello results list, select **Cezanne HR Software** and then select hello **Add** button tooadd hello application.</span></span>

    ![hello 결과 목록](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ecb80-137">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ecb80-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ecb80-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Cezanne HR 소프트웨어에서 Azure AD SSO를 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ecb80-139">SSO toowork에 대 한 Azure AD tooknow hello Cezanne HR 소프트웨어 대응 toohello Azure AD 사용자는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-139">For SSO toowork, Azure AD needs tooknow hello Cezanne HR software counterpart toohello Azure AD user.</span></span> <span data-ttu-id="ecb80-140">즉, hello Cezanne HR 소프트웨어에에서는 Azure AD 사용자 및 hello 관련된 사용자 간의 링크 관계를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-140">In other words, you must establish a link relationship between an Azure AD user and hello related user in hello Cezanne HR software.</span></span>

<span data-ttu-id="ecb80-141">tooestablish hello 링크 관계를 할당 hello Cezanne HR 소프트웨어 **사용자 이름** hello Azure AD로 값 **Username** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-141">tooestablish hello link relationship, assign hello Cezanne HR software **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="ecb80-142">tooconfigure 및 Azure AD SSO Cezanne HR 소프트웨어, 구성 요소를 다음 전체 hello를 사용 하 여 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-142">tooconfigure and test Azure AD SSO by using Cezanne HR software, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="ecb80-143">Azure AD SSO 구성</span><span class="sxs-lookup"><span data-stu-id="ecb80-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="ecb80-144">이 섹션에서는 Azure AD SSO hello Azure 포털에서에서 사용 하도록 설정 및 hello 다음을 수행 하 여 Cezanne HR 소프트웨어 응용 프로그램에서 SSO를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-144">In this section, you can enable Azure AD SSO in hello Azure portal and configure SSO in your Cezanne HR software application by doing hello following:</span></span>

1. <span data-ttu-id="ecb80-145">Hello hello에 Azure 포털에서에서 **Cezanne HR 소프트웨어** 응용 프로그램 통합 페이지에서 선택 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-145">In hello Azure portal, on hello **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![명령 "Single sign-on" hello][4]

2. <span data-ttu-id="ecb80-147">hello에 SSO, tooenable **Single sign on** 대화 상자, 선택 hello **모드** 으로 **SAML 기반 로그온**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-147">tooenable SSO, in hello **Single sign-on** dialog box, select hello **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![hello "모드" 상자](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="ecb80-149">아래 **Cezanne HR 소프트웨어 도메인 및 Url**, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-149">Under **Cezanne HR Software Domain and URLs**, do hello following:</span></span>

    ![hello "Cezanne HR 소프트웨어 도메인 및 Url" 섹션](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="ecb80-151">a.</span><span class="sxs-lookup"><span data-stu-id="ecb80-151">a.</span></span> <span data-ttu-id="ecb80-152">Hello에 **로그온 URL** 상자 구문 다음 hello에 URL을 입력 합니다.`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="ecb80-152">In hello **Sign-on URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="ecb80-153">b.</span><span class="sxs-lookup"><span data-stu-id="ecb80-153">b.</span></span> <span data-ttu-id="ecb80-154">Hello에 **회신 URL** 상자 구문 다음 hello에 URL을 입력 합니다.`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="ecb80-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="ecb80-155">hello 이전 값이 실제.</span><span class="sxs-lookup"><span data-stu-id="ecb80-155">hello preceding values are not real.</span></span> <span data-ttu-id="ecb80-156">Hello 실제 회신 URL 및 hello 로그온 URL을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-156">Update them with hello actual reply URL and hello sign-on URL.</span></span> <span data-ttu-id="ecb80-157">tooobtain hello 값, 연락처 hello [Cezanne HR 소프트웨어 클라이언트 지원 팀](mailto:info@cezannehr.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-157">tooobtain hello values, contact hello [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="ecb80-158">아래 **SAML 서명 인증서**선택, **인증서 (Base64)**, hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![hello "SAML 서명 인증서" 섹션](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="ecb80-160">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-160">Select **Save**.</span></span>

    ![hello "저장" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ecb80-162">아래 **Cezanne HR 소프트웨어 구성**선택, **Cezanne HR 소프트웨어 구성** tooopen hello **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="ecb80-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="ecb80-163">복사 hello **SAML 엔터티 ID** 및 **SAML Single Sign On 서비스** hello에서 URL **빠른 참조** 섹션.</span><span class="sxs-lookup"><span data-stu-id="ecb80-163">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service** URL from hello **Quick Reference** section.</span></span>

    ![hello "Cezanne HR 소프트웨어 구성" 섹션](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="ecb80-165">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Cezanne HR software 테 넌 트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-165">In a different web browser window, sign on tooyour Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="ecb80-166">Hello 왼쪽된 창에서 선택 **System 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-166">In hello left pane, select **System Setup**.</span></span> <span data-ttu-id="ecb80-167">**보안 설정** > **Single Sign-on 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![hello "Single Sign On 구성" 링크](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="ecb80-169">Hello에 **Single Sign-on (SSO) 서비스를 수행 하는 hello를 사용 하 여 사용자가 toolog 허용** 창, 선택 hello **SAML 2.0** 확인란과 선택 hello **고급 구성** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-169">In hello **Allow users toolog in using hello following Single Sign-On (SSO) services** pane, select hello **SAML 2.0** check box and select hello **Advanced Configuration** option.</span></span>

    ![Single Sign-On 서비스 옵션](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="ecb80-171">**새로 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-171">Select **Add New**.</span></span>

    ![hello "새로 추가" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="ecb80-173">아래 **SAML 2.0 Id 공급자**, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-173">Under **SAML 2.0 Identity Providers**, do hello following:</span></span>

    ![hello "SAML 2.0 Id 공급자" 섹션](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="ecb80-175">a.</span><span class="sxs-lookup"><span data-stu-id="ecb80-175">a.</span></span> <span data-ttu-id="ecb80-176">Hello에 **표시 이름** id 공급자의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-176">In hello **Display Name** box, enter hello name of your identity provider.</span></span>

    <span data-ttu-id="ecb80-177">b.</span><span class="sxs-lookup"><span data-stu-id="ecb80-177">b.</span></span> <span data-ttu-id="ecb80-178">Hello에 **엔터티 식별자** 상자, 붙여넣기 hello **SAML 엔터티 ID** hello Azure 포털에서에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-178">In hello **Entity Identifier** box, paste hello **SAML Entity ID** that you copied from hello Azure portal.</span></span> 

    <span data-ttu-id="ecb80-179">c.</span><span class="sxs-lookup"><span data-stu-id="ecb80-179">c.</span></span> <span data-ttu-id="ecb80-180">Hello에 **SAML 바인딩** 목록 상자 **POST**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-180">In hello **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="ecb80-181">d.</span><span class="sxs-lookup"><span data-stu-id="ecb80-181">d.</span></span> <span data-ttu-id="ecb80-182">Hello에 **보안 토큰 서비스 끝점** 상자, 붙여넣기 hello **SAML Single Sign On 서비스** hello Azure 포털에서에서 복사한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-182">In hello **Security Token Service Endpoint** box, paste hello **SAML Single Sign-On Service** URL that you copied from hello Azure portal.</span></span> 
    
    <span data-ttu-id="ecb80-183">e.</span><span class="sxs-lookup"><span data-stu-id="ecb80-183">e.</span></span> <span data-ttu-id="ecb80-184">Hello에 **사용자 ID 특성 이름** 상자에 입력 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-184">In hello **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="ecb80-185">f.</span><span class="sxs-lookup"><span data-stu-id="ecb80-185">f.</span></span> <span data-ttu-id="ecb80-186">Azure AD를 선택 하는 hello에서 인증서를 다운로드 하는 tooupload hello **업로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-186">tooupload hello downloaded certificate from Azure AD, select hello **Upload** button.</span></span>
    
    <span data-ttu-id="ecb80-187">g.</span><span class="sxs-lookup"><span data-stu-id="ecb80-187">g.</span></span> <span data-ttu-id="ecb80-188">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-188">Select **OK**.</span></span> 

12. <span data-ttu-id="ecb80-189">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-189">Select **Save**.</span></span>

    ![hello "저장" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="ecb80-191">Hello 지침 hello에서 앞의 간결한 버전을 읽을 수 hello 앱을 설정할 때 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-191">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ecb80-192">Hello에서 hello 앱을 추가한 다음 **Active Directory** > **엔터프라이즈 응용 프로그램** 섹션을 선택 하는 hello **Single sign on** 탭 합니다. 액세스 hello hello의 설명서를 포함 하는 후 **구성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="ecb80-192">After you add hello app from hello **Active Directory** > **Enterprise applications** section, select hello **Single sign-on** tab. Then access hello embedded documentation from hello **Configuration** section.</span></span> 

<span data-ttu-id="ecb80-193">hello 포함 된 설명서 기능에 대해 자세히 toolearn 참조 [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-193">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ecb80-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ecb80-194">Create an Azure AD test user</span></span>
<span data-ttu-id="ecb80-195">이 섹션에서는 테스트 사용자 Britta Simon hello Azure 포털에서에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-195">In this section, you create test user Britta Simon in hello Azure portal.</span></span>

![Britta Simon hello 테스트 사용자][100]

<span data-ttu-id="ecb80-197">Azure AD에서 테스트 사용자 toocreate 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-197">toocreate a test user in Azure AD, do hello following:</span></span>

1. <span data-ttu-id="ecb80-198">Hello에 **Azure 포털**hello 왼쪽된 창에서 선택 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-198">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![hello "Azure Active Directory" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ecb80-200">사용자 선택 toodisplay hello 목록 **사용자 및 그룹** > **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-200">toodisplay hello list of users, select **Users and groups** > **All users**.</span></span>
    
    !["모든 사용자" 링크를 hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="ecb80-202">hello **모든 사용자에 게** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-202">hello **All users** dialog box opens.</span></span>

3. <span data-ttu-id="ecb80-203">tooopen hello **사용자** 대화 상자에서 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-203">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![hello "추가" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ecb80-205">Hello에 **사용자** 대화 상자에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-205">In hello **User** dialog box, do hello following:</span></span>
 
    ![hello "User" 대화 상자](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ecb80-207">a.</span><span class="sxs-lookup"><span data-stu-id="ecb80-207">a.</span></span> <span data-ttu-id="ecb80-208">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ecb80-209">b.</span><span class="sxs-lookup"><span data-stu-id="ecb80-209">b.</span></span> <span data-ttu-id="ecb80-210">Hello에 **사용자 이름** 상자에 입력 사용자 Britta Simon **전자 메일 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-210">In hello **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="ecb80-211">c.</span><span class="sxs-lookup"><span data-stu-id="ecb80-211">c.</span></span> <span data-ttu-id="ecb80-212">선택 hello **암호 표시** 확인란을 선택한 다음 참고 hello 생성 된 값을 hello에 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-212">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="ecb80-213">d.</span><span class="sxs-lookup"><span data-stu-id="ecb80-213">d.</span></span> <span data-ttu-id="ecb80-214">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="ecb80-215">Cezanne HR 소프트웨어 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ecb80-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="ecb80-216">tooenable Azure AD 사용자가 toosign tooCezanne HR 소프트웨어에서 이러한 해야에 프로 비전 Cezanne HR 소프트웨어.</span><span class="sxs-lookup"><span data-stu-id="ecb80-216">tooenable Azure AD users toosign in tooCezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="ecb80-217">Hello Cezanne HR 소프트웨어의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-217">In hello case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="ecb80-218">Hello 다음을 수행 하 여 사용자 계정을 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-218">Provision a user account by doing hello following:</span></span>

1.  <span data-ttu-id="ecb80-219">관리자 권한으로 Cezanne HR software 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-219">Sign in tooyour Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="ecb80-220">Hello 왼쪽된 창에서 선택 **System 설치** > **사용자 관리** > **새 사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-220">In hello left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="ecb80-221">![hello "새 사용자 추가" 링크](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="ecb80-221">![hello "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="ecb80-222">**사용자 세부 정보**, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-222">Under **Person Details**, do hello following:</span></span>

    <span data-ttu-id="ecb80-223">!["사용자 세부 정보" 섹션 hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="ecb80-223">![hello "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="ecb80-224">a.</span><span class="sxs-lookup"><span data-stu-id="ecb80-224">a.</span></span> <span data-ttu-id="ecb80-225">**내부 사용자**를 **OFF**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="ecb80-226">b.</span><span class="sxs-lookup"><span data-stu-id="ecb80-226">b.</span></span> <span data-ttu-id="ecb80-227">Hello에 **이름** 상자, 형식 hello 사용자의 이름, 예를 들어 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-227">In hello **First Name** box, type hello user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="ecb80-228">c.</span><span class="sxs-lookup"><span data-stu-id="ecb80-228">c.</span></span> <span data-ttu-id="ecb80-229">Hello에 **성** 상자, 형식 hello 사용자의 성, 예를 들어 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-229">In hello **Last Name** box, type hello user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="ecb80-230">d.</span><span class="sxs-lookup"><span data-stu-id="ecb80-230">d.</span></span> <span data-ttu-id="ecb80-231">Hello에 **전자 메일** 상자 예를 들어 hello 사용자의 전자 메일 주소를 입력 합니다 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-231">In hello **E-mail** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="ecb80-232">아래 **계정 정보**, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-232">Under **Account Information**, do hello following:</span></span>

    <span data-ttu-id="ecb80-233">!["계정 정보" 섹션 hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="ecb80-233">![hello "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="ecb80-234">a.</span><span class="sxs-lookup"><span data-stu-id="ecb80-234">a.</span></span> <span data-ttu-id="ecb80-235">Hello에 **Username** 상자 예를 들어 hello 사용자의 전자 메일 주소를 입력 합니다 Brittasimon@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-235">In hello **Username** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="ecb80-236">b.</span><span class="sxs-lookup"><span data-stu-id="ecb80-236">b.</span></span> <span data-ttu-id="ecb80-237">Hello에 **암호** 상자 hello 사용자의 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-237">In hello **Password** box, type hello user's password.</span></span>
    
    <span data-ttu-id="ecb80-238">c.</span><span class="sxs-lookup"><span data-stu-id="ecb80-238">c.</span></span> <span data-ttu-id="ecb80-239">Hello에 **보안 역할** 상자 **HR Professional**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-239">In hello **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="ecb80-240">d.</span><span class="sxs-lookup"><span data-stu-id="ecb80-240">d.</span></span> <span data-ttu-id="ecb80-241">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-241">Select **OK**.</span></span>

5. <span data-ttu-id="ecb80-242">Hello에 **Single sign on** 탭 hello **SAML 2.0 식별자** 섹션에서 **새로 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-242">On hello **Single sign-on** tab, in hello **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="ecb80-243">![hello "새로 추가" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="ecb80-243">![hello "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="ecb80-244">Hello에 **Id 공급자** 목록 상자에서 id 공급자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-244">In hello **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="ecb80-245">Hello에 **사용자 식별자** 상자 테스트 사용자 Britta Simon의 계정에 대 한 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-245">In hello **User Identifier** box, enter hello email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="ecb80-246">!["Id 공급자" 및 "사용자 식별자" 상자 hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="ecb80-246">![hello "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="ecb80-247">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-247">Select **Save**.</span></span>

    <span data-ttu-id="ecb80-248">![hello "저장" 단추](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="ecb80-248">![hello "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ecb80-249">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-249">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ecb80-250">이 섹션에서는 액세스 tooCezanne HR 소프트웨어를 부여 하 여 테스트 사용자 Britta Simon toouse Azure SSO를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-250">In this section, you enable test user Britta Simon toouse Azure SSO by granting access tooCezanne HR software.</span></span>

![테스트 사용자 액세스][200] 

1. <span data-ttu-id="ecb80-252">Azure 포털 hello에 hello 응용 프로그램 보기를 열고 고 toohello 디렉터리 보기를 이동 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ecb80-252">In hello Azure portal, open hello applications view and then go toohello directory view.</span></span> <span data-ttu-id="ecb80-253">**엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-253">Select **Enterprise applications** > **All applications**.</span></span>

    !["모든 응용 프로그램" 링크를 hello][201] 

2. <span data-ttu-id="ecb80-255">Hello 응용 프로그램 목록에서 선택 **Cezanne HR 소프트웨어**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-255">In hello applications list, select **Cezanne HR Software**.</span></span>

    ![hello "응용 프로그램" 목록](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="ecb80-257">Hello hello 왼쪽 메뉴에서 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-257">In hello menu on hello left, select **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="ecb80-259">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-259">Select **Add**.</span></span> <span data-ttu-id="ecb80-260">그런 다음 hello **할당 추가** 대화 상자에서 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-260">Then in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][203]

5. <span data-ttu-id="ecb80-262">Hello에 **사용자 및 그룹** 대화 상자의 hello **사용자** 목록에서 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-262">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="ecb80-263">Hello에 **사용자 및 그룹** 대화 상자에서 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-263">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="ecb80-264">Hello에 **할당 추가** 대화 상자에서 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-264">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="ecb80-265">SSO 테스트</span><span class="sxs-lookup"><span data-stu-id="ecb80-265">Test SSO</span></span>

<span data-ttu-id="ecb80-266">이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD SSO 구성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-266">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="ecb80-267">Hello Cezanne HR 소프트웨어 타일 hello 액세스 패널을 선택 하면 자동으로 tooyour Cezanne HR 소프트웨어 응용 프로그램에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecb80-267">When you select hello Cezanne HR software tile in hello Access Panel, you sign on automatically tooyour Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecb80-268">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ecb80-268">Next steps</span></span>

* [<span data-ttu-id="ecb80-269">방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="ecb80-269">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ecb80-270">Azure Active Directory로 응용 프로그램 액세스 및 SSO란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ecb80-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png


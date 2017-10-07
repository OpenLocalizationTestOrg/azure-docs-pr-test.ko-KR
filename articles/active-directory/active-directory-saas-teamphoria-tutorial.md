---
title: "자습서: Teamphoria와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Teamphoria 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="42c4c-103">자습서: Teamphoria와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="42c4c-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="42c4c-104">이 자습서에 설명 어떻게 toointegrate Teamphoria Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42c4c-104">In this tutorial, you learn how toointegrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42c4c-105">다음 이점을 hello로 제공 Teamphoria Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="42c4c-105">Integrating Teamphoria with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="42c4c-106">액세스 tooTeamphoria을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-106">You can control in Azure AD who has access tooTeamphoria</span></span>
- <span data-ttu-id="42c4c-107">프로그램 사용자 tooautomatically get 로그온 tooTeamphoria (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-107">You can enable your users tooautomatically get signed-on tooTeamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42c4c-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="42c4c-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="42c4c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="42c4c-110">Prerequisites</span></span>

<span data-ttu-id="42c4c-111">다음 항목 hello가 필요 tooconfigure Teamphoria와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-111">tooconfigure Azure AD integration with Teamphoria, you need hello following items:</span></span>

- <span data-ttu-id="42c4c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="42c4c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42c4c-113">Teamphoria Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="42c4c-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42c4c-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42c4c-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42c4c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="42c4c-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42c4c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="42c4c-118">Scenario description</span></span>
<span data-ttu-id="42c4c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42c4c-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42c4c-121">Teamphoria는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="42c4c-121">Adding Teamphoria from hello gallery</span></span>
2. <span data-ttu-id="42c4c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="42c4c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-hello-gallery"></a><span data-ttu-id="42c4c-123">Teamphoria는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="42c4c-123">Adding Teamphoria from hello gallery</span></span>
<span data-ttu-id="42c4c-124">tooconfigure hello와의 통합 Teamphoria Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Teamphoria tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-124">tooconfigure hello integration of Teamphoria into Azure AD, you need tooadd Teamphoria from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="42c4c-125">**hello 갤러리에서 Teamphoria tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="42c4c-125">**tooadd Teamphoria from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="42c4c-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42c4c-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="42c4c-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="42c4c-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="42c4c-133">Hello 검색 상자에 입력 **Teamphoria**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-133">In hello search box, type **Teamphoria**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="42c4c-135">Hello 결과 패널에서 선택 **Teamphoria**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-135">In hello results panel, select **Teamphoria**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42c4c-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="42c4c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42c4c-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Teamphoria에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42c4c-139">Single sign on toowork에 대 한 Azure AD는 tooknow Teamphoria에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamphoria is tooa user in Azure AD.</span></span> <span data-ttu-id="42c4c-140">즉, Azure AD 사용자 및 Teamphoria에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-140">In other words, a link relationship between an Azure AD user and hello related user in Teamphoria needs toobe established.</span></span>

<span data-ttu-id="42c4c-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Teamphoria에 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamphoria.</span></span>

<span data-ttu-id="42c4c-142">tooconfigure 및 Teamphoria 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-142">tooconfigure and test Azure AD single sign-on with Teamphoria, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="42c4c-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="42c4c-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42c4c-145">**[Teamphoria 테스트 사용자 만들기](#creating-a-teamphoria-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Teamphoria에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - toohave a counterpart of Britta Simon in Teamphoria that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="42c4c-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42c4c-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="42c4c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42c4c-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="42c4c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42c4c-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 Teamphoria 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="42c4c-150">**tooconfigure Azure AD single sign on, Teamphoria와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="42c4c-150">**tooconfigure Azure AD single sign-on with Teamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="42c4c-151">Hello에 hello Azure 관리 포털에서 **Teamphoria** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-151">In hello Azure Management portal, on hello **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="42c4c-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="42c4c-155">Hello에 **Teamphoria 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-155">On hello **Teamphoria Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="42c4c-157">a.</span><span class="sxs-lookup"><span data-stu-id="42c4c-157">a.</span></span> <span data-ttu-id="42c4c-158">Hello에 **로그온 URL** 텍스트 패턴 hello를 사용 하 여 hello URL 입력:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="42c4c-158">In hello **Sign-on URL** textbox, type hello URL using hello following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="42c4c-159">이러한 없는지 hello 실제 값 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="42c4c-159">Please note that these are not hello real values.</span></span> <span data-ttu-id="42c4c-160">Tooupdate hello로 이러한 값이 있는 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-160">You have tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="42c4c-161">연락처 [Teamphoria 클라이언트 지원 팀](https://www.teamphoria.com/) tooget hello 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) tooget hello Sign-on URL.</span></span> 

4. <span data-ttu-id="42c4c-162">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="42c4c-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-164">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="42c4c-166">Hello에 **Teamphoria 구성** 섹션에서 클릭 **구성 Teamphoria** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="42c4c-166">On hello **Teamphoria Configuration** section, click **Configure Teamphoria** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="42c4c-167">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="42c4c-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="42c4c-169">tooconfigure single sign on에서 **Teamphoria** 쪽, 관리자 권한으로 로그인 tooyour Teamphoria 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-169">tooconfigure single sign-on on **Teamphoria** side, Login tooyour Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="42c4c-170">너무 이동**관리 설정** hello hello 구성 탭에서 클릭 하 고 hello 왼쪽된 도구 모음에서 옵션 **SINGLE SIGN-ON** tooopen hello SSO 구성 창.</span><span class="sxs-lookup"><span data-stu-id="42c4c-170">Go too**ADMIN SETTINGS** option in hello left toolbar and under hello hello Configure Tab click on **SINGLE SIGN-ON** tooopen hello SSO configuration window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="42c4c-172">클릭 **새 ID 공급자 추가** SSO에 대 한 hello 설정을 추가 하기 위한 hello tooopen hello 양식을 오른쪽 위 모서리에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-172">Click on **ADD NEW IDENTITY PROVIDER** option in hello top right corner tooopen hello form for adding hello settings for SSO.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="42c4c-174">아래에서 설명 된 대로 hello 필드에 대 한 hello 세부 정보 입력</span><span class="sxs-lookup"><span data-stu-id="42c4c-174">Enter hello details in hello fields as described below-</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="42c4c-176">a.</span><span class="sxs-lookup"><span data-stu-id="42c4c-176">a.</span></span> <span data-ttu-id="42c4c-177">**표시 이름** : hello 관리 페이지의 hello 플러그 인의 hello 표시 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-177">**DISPLAY NAME** : Enter hello display name of hello plugin on hello admin page.</span></span>

    <span data-ttu-id="42c4c-178">b.</span><span class="sxs-lookup"><span data-stu-id="42c4c-178">b.</span></span> <span data-ttu-id="42c4c-179">**단추 이름** : SSO를 통한 로그인에 대 한 hello 로그인 페이지에 표시 하는 hello 탭의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-179">**BUTTON NAME** : hello name of hello tab which will display on hello login page for logging in via SSO.</span></span>

    <span data-ttu-id="42c4c-180">c.</span><span class="sxs-lookup"><span data-stu-id="42c4c-180">c.</span></span> <span data-ttu-id="42c4c-181">**인증서** : 열기 hello 인증서 이전에 다운로드 한 hello hello의 복사 hello 내용 메모장에서 Azure 포털에서에서 동일 하 고 여기 hello 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-181">**CERTIFICATE** : Open hello Certificate downloaded earlier from hello Azure portal in notepad, copy hello contents of hello same and paste it here in hello box.</span></span>

    <span data-ttu-id="42c4c-182">d.</span><span class="sxs-lookup"><span data-stu-id="42c4c-182">d.</span></span> <span data-ttu-id="42c4c-183">**진입점** : 붙여넣기 hello **SAML Single Sign-on 서비스 URL** 이전 양식 hello Azure 포털을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-183">**ENTRY POINT** : Paste hello **SAML Single Sign-On Service URL** copied earlier form hello Azure portal.</span></span>

    <span data-ttu-id="42c4c-184">e.</span><span class="sxs-lookup"><span data-stu-id="42c4c-184">e.</span></span> <span data-ttu-id="42c4c-185">Hello 옵션을 너무 전환**ON** 을 클릭할 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-185">Switch hello option too**ON** and click on **SAVE**.</span></span> 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42c4c-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="42c4c-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="42c4c-187">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-187">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="42c4c-189">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="42c4c-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="42c4c-190">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-190">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42c4c-192">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-192">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42c4c-194">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="42c4c-194">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42c4c-196">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42c4c-198">a.</span><span class="sxs-lookup"><span data-stu-id="42c4c-198">a.</span></span> <span data-ttu-id="42c4c-199">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42c4c-200">b.</span><span class="sxs-lookup"><span data-stu-id="42c4c-200">b.</span></span> <span data-ttu-id="42c4c-201">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42c4c-202">c.</span><span class="sxs-lookup"><span data-stu-id="42c4c-202">c.</span></span> <span data-ttu-id="42c4c-203">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="42c4c-204">d.</span><span class="sxs-lookup"><span data-stu-id="42c4c-204">d.</span></span> <span data-ttu-id="42c4c-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="42c4c-206">Teamphoria 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="42c4c-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="42c4c-207">Tooenable Azure AD 사용자가 toolog Teamphoria로 주문 하 고에 Teamphoria에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-207">In order tooenable Azure AD users toolog into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="42c4c-208">Hello Teamphoria의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-208">In hello case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="42c4c-209">**사용자 계정 수행 tooprovision hello 다음 단계:**</span><span class="sxs-lookup"><span data-stu-id="42c4c-209">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="42c4c-210">관리자 권한으로 Teamphoria 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-210">Log in tooyour Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="42c4c-211">클릭 **관리자** hello 왼쪽된 도구 모음과 hello에서 설정이 **관리** 탭을 클릭 하 여 **사용자** tooopen hello admin 사용자가 페이지를 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-211">Click on **ADMIN** settings on hello left toolbar and under hello **MANAGE** tab Click on **USERS** tooopen hello admin page for users.</span></span>

    ![직원 추가](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="42c4c-213">Hello 클릭 **수동 초대** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-213">Click on hello **MANUAL INVITE** option.</span></span>

    ![피플 초대](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="42c4c-215">이 페이지에서 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-215">On this page, perform following action.</span></span> 
    
    ![피플 초대](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="42c4c-217">a.</span><span class="sxs-lookup"><span data-stu-id="42c4c-217">a.</span></span> <span data-ttu-id="42c4c-218">Hello에 **전자 메일 주소** textbox hello **전자 메일 주소** BrittaSimon입니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-218">In hello **EMAIL ADDRESS** textbox, hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42c4c-219">b.</span><span class="sxs-lookup"><span data-stu-id="42c4c-219">b.</span></span> <span data-ttu-id="42c4c-220">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-220">In hello **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="42c4c-221">c.</span><span class="sxs-lookup"><span data-stu-id="42c4c-221">c.</span></span> <span data-ttu-id="42c4c-222">Hello에 **성** 텍스트 상자에 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-222">In hello **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="42c4c-223">d.</span><span class="sxs-lookup"><span data-stu-id="42c4c-223">d.</span></span> <span data-ttu-id="42c4c-224">**1 사용자 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="42c4c-225">사용자가 tooaccept hello 초대 tooget hello 시스템에서 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-225">User needs tooaccept hello invite tooget created in hello system.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="42c4c-226">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="42c4c-227">이 섹션에서는 액세스 tooTeamphoria 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamphoria.</span></span>

![사용자 할당][200] 

<span data-ttu-id="42c4c-229">**tooassign Britta Simon tooTeamphoria hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="42c4c-229">**tooassign Britta Simon tooTeamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="42c4c-230">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-230">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="42c4c-232">Hello 응용 프로그램 목록에서 선택 **Teamphoria**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-232">In hello applications list, select **Teamphoria**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="42c4c-234">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="42c4c-236">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-236">Click **Add** button.</span></span> <span data-ttu-id="42c4c-237">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="42c4c-239">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="42c4c-240">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42c4c-241">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42c4c-242">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="42c4c-242">Testing single sign-on</span></span>

<span data-ttu-id="42c4c-243">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="42c4c-244">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="42c4c-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="42c4c-245">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42c4c-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="42c4c-246">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="42c4c-246">Additional resources</span></span>

* [<span data-ttu-id="42c4c-247">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="42c4c-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42c4c-248">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="42c4c-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png


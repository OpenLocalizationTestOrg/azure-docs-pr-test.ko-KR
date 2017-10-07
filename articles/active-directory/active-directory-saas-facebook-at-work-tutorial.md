---
title: "자습서: Workplace by Facebook과 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Facebook에서 회사 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="203df-103">자습서: Workplace by Facebook과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="203df-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="203df-104">이 자습서에 설명 어떻게 toointegrate Facebook Azure Active directory (Azure AD)에서 작업 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="203df-105">Facebook에서 작업 공간을 Azure AD와 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="203df-106">Facebook에서 액세스 tooWorkplace을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203df-106">You can control in Azure AD who has access tooWorkplace by Facebook.</span></span>
- <span data-ttu-id="203df-107">Tooautomatically 로그 tooWorkplace에 Facebook (single sign on)에서 자신의 Azure AD 계정을 가진 사용자가 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203df-107">You can enable your users tooautomatically get signed on tooWorkplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="203df-108">하나의 중앙 위치에 사용자 계정을 관리할 수 있습니다: Azure 포털 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="203df-109">Azure AD와의 SaaS(Software as a Service) 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="203df-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="203df-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="203df-110">Prerequisites</span></span>

<span data-ttu-id="203df-111">Facebook에서 작업 공간와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="203df-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="203df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="203df-113">Workplace by Facebook SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="203df-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="203df-114">이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="203df-114">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="203df-115">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="203df-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="203df-116">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203df-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="203df-117">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="203df-117">Scenario description</span></span>
<span data-ttu-id="203df-118">이 자습서에서는 테스트 환경에서 Azure AD SSO를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="203df-119">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203df-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="203df-120">Hello 갤러리에서 Facebook에서 작업 공간을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-120">Add Workplace by Facebook from hello gallery.</span></span>
2. <span data-ttu-id="203df-121">Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="203df-122">Facebook에서 작업 공간 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="203df-122">Add Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="203df-123">Azure AD Facebook에서 작업 공간으로 tooconfigure hello 통합 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Facebook에서 작업 공간을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-123">tooconfigure hello integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="203df-124">Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 창에서 선택 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-124">In hello [Azure portal](https://portal.azure.com), in hello left pane, select **Azure Active Directory**.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="203df-126">너무 찾아보기**엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-126">Browse too**Enterprise applications** > **All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="203df-128">tooadd hello 새 응용 프로그램을 선택 **새 응용 프로그램** hello hello 대화 상자 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203df-128">tooadd hello new application, select **New application** on hello top of hello dialog box.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="203df-130">Hello 검색 상자에 입력 **Facebook에서 작업 공간**를 선택 하 고 **Facebook에서 작업 공간** 결과에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-130">In hello search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="203df-131">그런 다음 선택 **추가**, tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-131">Then select **Add**, tooadd hello application.</span></span>

    ![Facebook에서 작업 공간 hello 결과 목록에서](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="203df-133">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="203df-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="203df-134">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Workplace by Facebook에서 Azure AD SSO를 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="203df-135">SSO toowork에 대 한 Azure AD는 tooknow Facebook에서 직장에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-135">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="203df-136">즉, Azure AD 사용자 및 Facebook에서 직장에서 hello 관련된 사용자 간에 연결 된 관계를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-136">In other words, a linked relationship between an Azure AD user and hello related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="203df-137">Hello hello 값을 할당 하 여이 관계를 설정할 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Facebook에서 직장에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-137">Establish this relationship by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="203df-138">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="203df-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="203df-139">이 섹션에서는 hello Azure 포털에서에서 Azure AD SSO를 사용 하 고 회사에서 Facebook 응용 프로그램에서 SSO를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-139">In this section, you enable Azure AD SSO in hello Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="203df-140">Hello hello에 Azure 포털에서에서 **Facebook에서 작업 공간** 응용 프로그램 통합 페이지에서 선택 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-140">In hello Azure portal, on hello **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="203df-142">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable SSO 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-142">In hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="203df-144">Hello에 **Facebook 도메인 및 Url에서 작업 공간** 섹션에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="203df-144">In hello **Workplace by Facebook Domain and URLs** section, do hello following:</span></span>

    <span data-ttu-id="203df-145">a.</span><span class="sxs-lookup"><span data-stu-id="203df-145">a.</span></span> <span data-ttu-id="203df-146">Hello에 **로그온 URL** 입력란 hello 패턴을 사용 하는 URL을 입력 합니다.`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="203df-146">In hello **Sign-on URL** text box, type a URL that uses hello following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="203df-147">b.</span><span class="sxs-lookup"><span data-stu-id="203df-147">b.</span></span> <span data-ttu-id="203df-148">Hello에 **식별자** 입력란 hello 패턴을 사용 하는 URL을 입력 합니다.`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="203df-148">In hello **Identifier** text box, type a URL that uses hello following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="203df-149">이러한 값은 예제일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-149">These values are an example only.</span></span> <span data-ttu-id="203df-150">Hello 실제 로그온 URL과 식별자와 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-150">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="203df-151">연락처 hello [Facebook 클라이언트 지원 팀에서 작업 공간](https://workplace.fb.com/faq/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-151">Contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="203df-152">Hello에 **SAML 서명 인증서** 섹션에서 **인증서 (Base64)**, hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-152">In hello **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="203df-154">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-154">Select **Save**.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="203df-156">Hello에 **Facebook 구성 하 여 작업 공간** 섹션에서 **Facebook에서 작업 공간 구성** tooopen hello **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="203df-156">In hello **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="203df-157">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조** 섹션.</span><span class="sxs-lookup"><span data-stu-id="203df-157">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Workplace by Facebook 구성](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="203df-159">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Facebook 회사 사이트에서 작업 공간에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-159">In a different web browser window, sign in tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="203df-160">Hello SAML 인증 프로세스의 일환으로, 순서 toopass 매개 변수 tooAzure AD 크기에 쿼리 문자열을 too2.5 킬로바이트를 작업 공간 צ ְ ײ 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-160">As part of hello SAML authentication process, Workplace can use query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="203df-161">Hello에 **회사 대시보드**, toohello 이동 **인증** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-161">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="203df-162">아래 **SAML 인증**선택, **SSO만** hello 드롭 다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-162">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="203df-163">Hello에서 복사 된 hello 값 입력 **Facebook 구성 하 여 작업 공간** hello hello 해당 필드에 Azure 포털의 섹션:</span><span class="sxs-lookup"><span data-stu-id="203df-163">Enter hello values copied from hello **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="203df-164">에 **SAML URL** 붙여넣기 hello 값의 텍스트 상자 **Single Sign-on 서비스 URL**, hello Azure 포털에서에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-164">In the **SAML URL** text box, paste hello value of **Single Sign-On Service URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="203df-165">에 **SAML 발급자 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, hello Azure 포털에서에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-165">In the **SAML Issuer URL** text box, paste hello value of **SAML Entity ID**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="203df-166">**SAML 로그 아웃 리디렉션 (선택 사항)**의 hello 값을 붙여 **Sign-Out URL**, hello Azure 포털에서에서 복사한 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-166">In **SAML Logout Redirect (optional)**, paste hello value of **Sign-Out URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="203df-167">Open 프로그램 **e-64로 인코딩된 인증서** 메모장에서 hello Azure 포털에서에서 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-167">Open your **base-64 encoded certificate** in Notepad, downloaded from hello Azure portal.</span></span> <span data-ttu-id="203df-168">Hello 내용을 클립보드에 복사한 다음 toothe **SAML 인증서** 입력란.</span><span class="sxs-lookup"><span data-stu-id="203df-168">Copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="203df-169">Tooenter hello audience 해야 URL, 받는 사람 URL 및 ACS (Assertion Consumer Service) hello 아래 나열 된 URL **SAML 구성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="203df-169">You might need tooenter hello audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="203df-170">Hello 섹션의 toohello 아래쪽 스크롤하여 선택 **테스트 SSO**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-170">Scroll toohello bottom of hello section, and select **Test SSO**.</span></span> <span data-ttu-id="203df-171">Hello Azure AD 로그인 페이지와 팝업 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="203df-171">A pop-up window appears, with hello Azure AD sign-in page.</span></span> <span data-ttu-id="203df-172">tooauthenticate를 일반적인 방법으로 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-172">tooauthenticate, enter your credentials as normal.</span></span> <span data-ttu-id="203df-173">Azure AD에서 다시 반환 하는 hello 전자 메일 주소는 로그인 하는 작업 공간 계정을 hello와 동일 hello는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-173">Ensure hello email address returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="203df-174">Hello 페이지를 선택 toohello 아래쪽을 스크롤할 hello 테스트가 성공적으로 완료 되 면 있으면 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-174">If hello test has finished successfully, scroll toohello bottom of hello page and select **Save**.</span></span>

14. <span data-ttu-id="203df-175">Workplace를 사용하는 모든 사용자에게 이제 인증을 위한 Azure AD 로그인 페이지가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="203df-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="203df-176">SAML 로그 아웃 URL 로그 아웃 페이지 hello Azure AD에 사용 되는 toopoint 될 수 있는 tooconfigure를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203df-176">You can choose tooconfigure a SAML sign out URL, which can be used toopoint at hello Azure AD sign-out page.</span></span> <span data-ttu-id="203df-177">이 설정을 사용 하도록 설정 및 구성 된 경우 hello 사용자가 더 이상 toohello 방향이 지정 된 작업 공간에 대 한 로그 아웃 페이지.</span><span class="sxs-lookup"><span data-stu-id="203df-177">When this setting is enabled and configured, hello user is no longer directed toohello Workplace sign-out page.</span></span> <span data-ttu-id="203df-178">대신, hello 사용자는 hello SAML 로그 아웃 리디렉션 설정에 추가 된 리디렉션된 toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-178">Instead, hello user is redirected toohello URL that was added in hello SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="203df-179">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면, 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app.</span></span> <span data-ttu-id="203df-180">Hello에서이 앱을 추가한 후 **Active Directory** > **엔터프라이즈 응용 프로그램** 섹션에서 선택 하기만 하면 hello **Single Sign On** 탭 및 액세스 hello hello 통해 설명서에 포함 된 **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="203df-180">After adding this app from hello **Active Directory** > **Enterprise Applications** section, simply select hello **Single Sign-On** tab, and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="203df-181">자세한 내용은 hello 포함 된 설명서 기능 hello에 대 한 [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-181">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="203df-182">재인증 빈도 구성</span><span class="sxs-lookup"><span data-stu-id="203df-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="203df-183">SAML 확인을 3 일 동안 매일 1 주, 2 주, 1 개월에 대 한 작업 공간 tooprompt를 구성할 수 있습니다 또는 never입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-183">You can configure Workplace tooprompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="203df-184">hello 모바일 응용 프로그램에 대해 hello SAML 확인에 대 한 최소 값은 설정 tooone 주입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-184">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="203df-185">모든 사용자에 대해 강제로 SAML 재설정을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203df-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="203df-186">toodo이를 사용 하 여 hello **필요 SAML 인증 모든 사용자에 게 이제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-186">toodo this, use hello **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="203df-187">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="203df-187">Create an Azure AD test user</span></span>
<span data-ttu-id="203df-188">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

1. <span data-ttu-id="203df-190">Hello에 **Azure 포털**hello 왼쪽된 창에서 선택 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-190">In hello **Azure portal**, in hello left pane, select **Azure Active Directory**.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="203df-192">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 선택 하 고 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-192">toodisplay hello list of users, go too**Users and groups**, and select **All users**.</span></span>
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="203df-194">tooopen hello **사용자** 대화 상자에서 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-194">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![hello 추가 단추](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="203df-196">Hello에 **사용자** 대화 상자에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="203df-196">In hello **User** dialog box, do hello following:</span></span>
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="203df-198">a.</span><span class="sxs-lookup"><span data-stu-id="203df-198">a.</span></span> <span data-ttu-id="203df-199">Hello에 **이름** 텍스트 상자에서 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-199">In hello **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="203df-200">b.</span><span class="sxs-lookup"><span data-stu-id="203df-200">b.</span></span> <span data-ttu-id="203df-201">Hello에 **사용자 이름** 텍스트 상자, 형식 hello **전자 메일 주소** BrittaSimon입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-201">In hello **User name** text box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="203df-202">c.</span><span class="sxs-lookup"><span data-stu-id="203df-202">c.</span></span> <span data-ttu-id="203df-203">**암호 표시**를 선택하고 암호를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="203df-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="203df-204">d.</span><span class="sxs-lookup"><span data-stu-id="203df-204">d.</span></span> <span data-ttu-id="203df-205">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="203df-206">Workplace by Facebook 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="203df-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="203df-207">이 섹션에서는 Workplace by Facebook에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="203df-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="203df-208">Workplace by Facebook은 기본적으로 사용하도록 설정된 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="203df-209">이 섹션에는 사용자의 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="203df-209">There is no action for you in this section.</span></span> <span data-ttu-id="203df-210">사용자가 Facebook에서 작업 공간에 존재 하지 않으면 새 Facebook에서 작업 공간 tooaccess 할 때 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="203df-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="203df-211">Toocreate 사용자를 수동으로 필요한 경우 문의 hello [Facebook 클라이언트 지원 팀에서 작업 공간](https://workplace.fb.com/faq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-211">If you need toocreate a user manually, contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="203df-212">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-212">Assign hello Azure AD test user</span></span>

<span data-ttu-id="203df-213">이 섹션에서는 Facebook에서 tooWorkplace 액세스 권한을 부여 하 여 Britta Simon toouse Azure SSO를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-213">In this section, you enable Britta Simon toouse Azure SSO by granting access tooWorkplace by Facebook.</span></span>

![사용자 할당][200] 

1. <span data-ttu-id="203df-215">Hello Azure 포털을 열고 hello 응용 프로그램 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="203df-215">In hello Azure portal, open hello applications view.</span></span> <span data-ttu-id="203df-216">Toohello 디렉터리 보기, 너무 이동**엔터프라이즈 응용 프로그램**를 선택한 후 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-216">Go toohello directory view, go too**Enterprise applications**, and then select **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="203df-218">Hello 응용 프로그램 목록에서 선택 **Facebook에서 작업 공간**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-218">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![hello 응용 프로그램 목록에서 Facebook 링크 하 여 작업 공간 hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="203df-220">Hello hello 왼쪽 메뉴에서 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-220">In hello menu on hello left, select **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="203df-222">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-222">Select **Add**.</span></span> <span data-ttu-id="203df-223">그런 다음, hello **할당 추가** 창 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-223">Then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="203df-225">Hello에 **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203df-225">In hello **Users and groups** dialog box, select **Britta Simon** in hello users list.</span></span>

6. <span data-ttu-id="203df-226">Hello에 **사용자 및 그룹** 대화 상자에서 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-226">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="203df-227">Hello에 **할당 추가** 대화 상자에서 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-227">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="203df-228">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="203df-228">Test single sign-on</span></span>

<span data-ttu-id="203df-229">SSO 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="203df-229">If you want tootest your SSO settings, open hello Access Panel.</span></span>
<span data-ttu-id="203df-230">자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-230">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="203df-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="203df-231">Next steps</span></span>

* <span data-ttu-id="203df-232">Hello 참조 [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-232">See hello [list of tutorials on how toointegrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="203df-233">[Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="203df-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="203df-234">너무 방법에 대 한 자세한[사용자 프로비저닝을 구성할](active-directory-saas-facebook-at-work-provisioning-tutorial.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="203df-234">Learn more about how too[configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png


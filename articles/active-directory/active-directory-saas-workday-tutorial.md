---
title: "자습서: Workday와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Workday 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="60028-103">자습서: Workday와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="60028-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="60028-104">이 자습서에 설명 어떻게 toointegrate Workday Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60028-104">In this tutorial, you learn how toointegrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60028-105">Azure AD와 Workday 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-105">Integrating Workday with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="60028-106">액세스 tooWorkday을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-106">You can control in Azure AD who has access tooWorkday</span></span>
- <span data-ttu-id="60028-107">프로그램 사용자 tooautomatically get 로그온 tooWorkday (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-107">You can enable your users tooautomatically get signed-on tooWorkday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60028-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="60028-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60028-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="60028-110">Prerequisites</span></span>

<span data-ttu-id="60028-111">Azure AD 및 Workday 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-111">tooconfigure Azure AD integration with Workday, you need hello following items:</span></span>

- <span data-ttu-id="60028-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="60028-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60028-113">Workday Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="60028-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60028-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60028-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60028-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="60028-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60028-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60028-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="60028-118">Scenario description</span></span>
<span data-ttu-id="60028-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60028-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60028-121">Workday는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="60028-121">Adding Workday from hello gallery</span></span>
2. <span data-ttu-id="60028-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="60028-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-hello-gallery"></a><span data-ttu-id="60028-123">Workday는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="60028-123">Adding Workday from hello gallery</span></span>
<span data-ttu-id="60028-124">tooconfigure hello와의 통합 Workday Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd Workday 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-124">tooconfigure hello integration of Workday into Azure AD, you need tooadd Workday from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="60028-125">**hello 갤러리에서 Workday tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="60028-125">**tooadd Workday from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="60028-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="60028-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="60028-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="60028-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="60028-133">Hello 검색 상자에 입력 **Workday**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-133">In hello search box, type **Workday**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="60028-135">Hello 결과 패널에서 선택 **Workday**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-135">In hello results panel, select **Workday**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60028-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="60028-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60028-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Workday에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="60028-139">Single sign on toowork에 대 한 Azure AD는 tooknow Workday의 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workday is tooa user in Azure AD.</span></span> <span data-ttu-id="60028-140">즉, Azure AD 사용자 및 Workday의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-140">In other words, a link relationship between an Azure AD user and hello related user in Workday needs toobe established.</span></span>

<span data-ttu-id="60028-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Workday의 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workday.</span></span>

<span data-ttu-id="60028-142">tooconfigure 및 근무 시간을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-142">tooconfigure and test Azure AD single sign-on with Workday, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="60028-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="60028-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60028-145">**[Workday 테스트 사용자 만들기](#creating-a-workday-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 업무 시간에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - toohave a counterpart of Britta Simon in Workday that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="60028-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60028-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="60028-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60028-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="60028-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="60028-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Workday 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="60028-150">**tooconfigure Azure AD single sign on, workday hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="60028-150">**tooconfigure Azure AD single sign-on with Workday, perform hello following steps:**</span></span>

1. <span data-ttu-id="60028-151">Hello hello에 Azure 포털에서에서 **Workday** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-151">In hello Azure portal, on hello **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="60028-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="60028-155">Hello에 **Workday 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-155">On hello **Workday Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="60028-157">a.</span><span class="sxs-lookup"><span data-stu-id="60028-157">a.</span></span> <span data-ttu-id="60028-158">Hello에 **로그온 URL** 형식 hello 값으로 텍스트 상자:`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="60028-158">In hello **Sign-on URL** textbox, type hello value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="60028-159">b.</span><span class="sxs-lookup"><span data-stu-id="60028-159">b.</span></span> <span data-ttu-id="60028-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="60028-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="60028-161">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-161">These values are not hello real.</span></span> <span data-ttu-id="60028-162">Hello 실제 로그온 URL와 회신 URL이 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="60028-163">회신 URL에 하위 도메인(예: www, wd2, wd3, wd3-impl, wd5, wd5-impl)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="60028-164">"*http://www.myworkday.com*"과 같은 것은 작동하지만 "*http://myworkday.com*"은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="60028-165">연락처 [클라이언트 Workday 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget these values.</span></span> 
 

4. <span data-ttu-id="60028-166">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="60028-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="60028-170">Hello에 **Workday 구성** 섹션에서 클릭 **Workday 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="60028-170">On hello **Workday Configuration** section, click **Configure Workday** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="60028-171">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="60028-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="60028-172">![Single Sign-On 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="60028-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="60028-173">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Workday 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-173">In a different web browser window, log in tooyour Workday company site as an administrator.</span></span>

8. <span data-ttu-id="60028-174">너무 이동**메뉴 \> 워크 벤치**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-174">Go too**Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="60028-175">![워크벤치](./media/active-directory-saas-workday-tutorial/IC782923.png "워크벤치")</span><span class="sxs-lookup"><span data-stu-id="60028-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="60028-176">너무 이동**계정 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-176">Go too**Account Administration**.</span></span>
   
    <span data-ttu-id="60028-177">![계정 관리](./media/active-directory-saas-workday-tutorial/IC782924.png "계정 관리")</span><span class="sxs-lookup"><span data-stu-id="60028-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="60028-178">너무 이동**테 넌 트 설정 편집-보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-178">Go too**Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="60028-179">![테넌트 보안 편집](./media/active-directory-saas-workday-tutorial/IC782925.png "테넌트 보안 편집")</span><span class="sxs-lookup"><span data-stu-id="60028-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="60028-180">Hello에 **리디렉션 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-180">In hello **Redirection URLs** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="60028-181">![리디렉션 URL](./media/active-directory-saas-workday-tutorial/IC7829581.png "리디렉션 URL")</span><span class="sxs-lookup"><span data-stu-id="60028-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="60028-182">a.</span><span class="sxs-lookup"><span data-stu-id="60028-182">a.</span></span> <span data-ttu-id="60028-183">**행 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="60028-184">b.</span><span class="sxs-lookup"><span data-stu-id="60028-184">b.</span></span> <span data-ttu-id="60028-185">Hello에 **로그인 리디렉션 URL** 텍스트 상자 및 hello **모바일 리디렉션 URL** 텍스트 형식 hello **로그온 URL** hello에 입력 한 **Workday 도메인 및 Url** hello Azure 포털의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-185">In hello **Login Redirect URL** textbox and hello **Mobile Redirect URL** textbox, type hello **Sign-on URL** you have entered on hello **Workday Domain and URLs** section of hello Azure portal.</span></span>
   
    <span data-ttu-id="60028-186">c.</span><span class="sxs-lookup"><span data-stu-id="60028-186">c.</span></span> <span data-ttu-id="60028-187">Hello hello에 Azure 포털에서에서 **sign on 구성** 창, 복사 hello **Sign-Out URL**, 다음 hello에 붙여 넣는 **로그 아웃 리디렉션 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-187">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL**, and then paste it into hello **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="60028-188">d.</span><span class="sxs-lookup"><span data-stu-id="60028-188">d.</span></span>  <span data-ttu-id="60028-189">**환경** 형식 hello 환경 이름 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-189">In **Environment** textbox, type hello environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="60028-190">hello hello 환경 특성의 값은 연결 되어 hello 테 넌 트 URL의 toohello 값:</span><span class="sxs-lookup"><span data-stu-id="60028-190">hello value of hello Environment attribute is tied toohello value of hello tenant URL:</span></span>  
    ><span data-ttu-id="60028-191">-Hello Workday 테 넌 트 URL의 hello 도메인 이름이 impl로 예를 들어 시작: *https://impl.workday.com/\<테 넌 트\>/login-saml2.htmld*), hello **환경** 특성 tooImplementation 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-191">-If hello domain name of hello Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **Environment** attribute must be set tooImplementation.</span></span>  
    ><span data-ttu-id="60028-192">-Hello 도메인 이름이 이와 다르게 시작, 해야 toocontact [클라이언트 Workday 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello 일치 **환경** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-192">-If hello domain name starts with something else, you need toocontact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello matching **Environment** value.</span></span>

12. <span data-ttu-id="60028-193">Hello에 **SAML 설정** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-193">In hello **SAML Setup** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="60028-194">![SAML 설정](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="60028-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="60028-195">a.</span><span class="sxs-lookup"><span data-stu-id="60028-195">a.</span></span>  <span data-ttu-id="60028-196">**SAML 인증 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="60028-197">b.</span><span class="sxs-lookup"><span data-stu-id="60028-197">b.</span></span>  <span data-ttu-id="60028-198">**행 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="60028-199">Hello SAML Id 공급자 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-199">In hello SAML Identity Providers section, perform hello following steps:</span></span>
   
    <span data-ttu-id="60028-200">![SAML ID 공급자](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML ID 공급자")</span><span class="sxs-lookup"><span data-stu-id="60028-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="60028-201">a.</span><span class="sxs-lookup"><span data-stu-id="60028-201">a.</span></span> <span data-ttu-id="60028-202">Hello Id 공급자 이름 텍스트 상자에 공급자 이름을 입력 합니다 (예: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="60028-202">In hello Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="60028-203">b.</span><span class="sxs-lookup"><span data-stu-id="60028-203">b.</span></span> <span data-ttu-id="60028-204">Hello hello에 Azure 포털에서에서 **sign on 구성** 창, 복사 hello **SAML 엔터티 ID** 값을 복사한 다음 hello에 붙여 넣을 **발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-204">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Entity ID** value, and then paste it into hello **Issuer** textbox.</span></span>
   
    <span data-ttu-id="60028-205">c.</span><span class="sxs-lookup"><span data-stu-id="60028-205">c.</span></span> <span data-ttu-id="60028-206">**Enable Workday Initiated Logout**(Workday에서 시작된 로그아웃 사용)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="60028-207">d.</span><span class="sxs-lookup"><span data-stu-id="60028-207">d.</span></span> <span data-ttu-id="60028-208">Hello hello에 Azure 포털에서에서 **sign on 구성** 창, 복사 hello **Sign-Out URL** 값을 복사한 다음 hello에 붙여 넣을 **로그 아웃 요청 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-208">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL** value, and then paste it into hello **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="60028-209">e.</span><span class="sxs-lookup"><span data-stu-id="60028-209">e.</span></span> <span data-ttu-id="60028-210">**ID 공급자 공개 키 인증서**를 클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="60028-211">![만들기](./media/active-directory-saas-workday-tutorial/IC782928.png "만들기")</span><span class="sxs-lookup"><span data-stu-id="60028-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="60028-212">f.</span><span class="sxs-lookup"><span data-stu-id="60028-212">f.</span></span> <span data-ttu-id="60028-213">**x509 공개 키 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="60028-214">![만들기](./media/active-directory-saas-workday-tutorial/IC782929.png "만들기")</span><span class="sxs-lookup"><span data-stu-id="60028-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="60028-215">Hello에 **x509 공개 키 보기** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-215">In hello **View x509 Public Key** section, perform hello following steps:</span></span> 
   
    <span data-ttu-id="60028-216">![x509 공개 키 보기](./media/active-directory-saas-workday-tutorial/IC782930.png "x509 공개 키 보기")</span><span class="sxs-lookup"><span data-stu-id="60028-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="60028-217">a.</span><span class="sxs-lookup"><span data-stu-id="60028-217">a.</span></span> <span data-ttu-id="60028-218">Hello에 **이름** 텍스트 상자에, 인증서 이름 입력 (예: *PPE\_SP*).</span><span class="sxs-lookup"><span data-stu-id="60028-218">In hello **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="60028-219">b.</span><span class="sxs-lookup"><span data-stu-id="60028-219">b.</span></span> <span data-ttu-id="60028-220">Hello에 **Valid From** 텍스트 형식 hello 인증서의 특성 값에서 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-220">In hello **Valid From** textbox, type hello valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="60028-221">c.</span><span class="sxs-lookup"><span data-stu-id="60028-221">c.</span></span>  <span data-ttu-id="60028-222">Hello에 **Valid To** 텍스트 상자에 인증서의 형식 hello 유효한 tooattribute 값입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-222">In hello **Valid To** textbox, type hello valid tooattribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="60028-223">날짜부터 유효 hello를 가져올 수 있으며 두 번 클릭 하 여 hello 다운로드 한 인증서에서 유효한 toodate hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-223">You can get hello valid from date and hello valid toodate from hello downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="60028-224">hello 날짜 hello 아래에 나열 됩니다 **세부 정보** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-224">hello dates are listed under hello **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="60028-225">d.</span><span class="sxs-lookup"><span data-stu-id="60028-225">d.</span></span>  <span data-ttu-id="60028-226">메모장을 선택한 다음의 콘텐츠 복사 hello에서 e-64로 인코딩된 인증서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="60028-226">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   
    <span data-ttu-id="60028-227">e.</span><span class="sxs-lookup"><span data-stu-id="60028-227">e.</span></span>  <span data-ttu-id="60028-228">Hello에 **인증서** 붙여넣기 hello 내용 클립보드의 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-228">In hello **Certificate** textbox, paste hello content of your clipboard.</span></span>
   
    <span data-ttu-id="60028-229">f.</span><span class="sxs-lookup"><span data-stu-id="60028-229">f.</span></span>  <span data-ttu-id="60028-230">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-230">Click **OK**.</span></span>

15. <span data-ttu-id="60028-231">Hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-231">Perform hello following steps:</span></span> 
   
    <span data-ttu-id="60028-232">![SSO 구성](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO 구성")</span><span class="sxs-lookup"><span data-stu-id="60028-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="60028-233">a.</span><span class="sxs-lookup"><span data-stu-id="60028-233">a.</span></span>  <span data-ttu-id="60028-234">Hello를 사용 하도록 설정 **x509 개인 키 쌍**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-234">Enable hello **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="60028-235">b.</span><span class="sxs-lookup"><span data-stu-id="60028-235">b.</span></span>  <span data-ttu-id="60028-236">Hello에 **서비스 공급자 ID** 텍스트 상자에 **http://www.workday.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-236">In hello **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="60028-237">c.</span><span class="sxs-lookup"><span data-stu-id="60028-237">c.</span></span>  <span data-ttu-id="60028-238">**SP가 시작한 SAML 인증 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="60028-239">d.</span><span class="sxs-lookup"><span data-stu-id="60028-239">d.</span></span>  <span data-ttu-id="60028-240">Hello hello에 Azure 포털에서에서 **sign on 구성** 창, 복사 hello **SAML Single Sign-on 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **IdP SSO 서비스 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-240">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="60028-241">e.</span><span class="sxs-lookup"><span data-stu-id="60028-241">e.</span></span> <span data-ttu-id="60028-242">**SP에서 시작한 인증 요청을 Deflate하지 않음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="60028-243">f.</span><span class="sxs-lookup"><span data-stu-id="60028-243">f.</span></span> <span data-ttu-id="60028-244">**인증 요청 서명 메서드**로 **SHA256**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="60028-245">![인증 요청 서명 메서드](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "인증 요청 서명 메서드")</span><span class="sxs-lookup"><span data-stu-id="60028-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="60028-246">g.</span><span class="sxs-lookup"><span data-stu-id="60028-246">g.</span></span> <span data-ttu-id="60028-247">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="60028-248">![확인](./media/active-directory-saas-workday-tutorial/IC782933.png "확인")
<CE></span><span class="sxs-lookup"><span data-stu-id="60028-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="60028-249">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="60028-249">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="60028-250">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="60028-250">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="60028-251">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="60028-251">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60028-252">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="60028-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="60028-253">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-253">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="60028-255">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="60028-255">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="60028-256">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="60028-256">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="60028-258">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-258">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="60028-260">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-260">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60028-262">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-262">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60028-264">a.</span><span class="sxs-lookup"><span data-stu-id="60028-264">a.</span></span> <span data-ttu-id="60028-265">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-265">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60028-266">b.</span><span class="sxs-lookup"><span data-stu-id="60028-266">b.</span></span> <span data-ttu-id="60028-267">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-267">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60028-268">c.</span><span class="sxs-lookup"><span data-stu-id="60028-268">c.</span></span> <span data-ttu-id="60028-269">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-269">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="60028-270">d.</span><span class="sxs-lookup"><span data-stu-id="60028-270">d.</span></span> <span data-ttu-id="60028-271">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="60028-272">Workday 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="60028-272">Creating a Workday test user</span></span>

<span data-ttu-id="60028-273">테스트 사용자가 Workday에 프로 비전 tooget 해야 toocontact hello [클라이언트 Workday 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-273">tooget a test user provisioned into Workday, you need toocontact hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="60028-274">hello [클라이언트 Workday 지원 팀](https://www.workday.com/en-us/partners-services/services/support.html) hello 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60028-274">hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates hello user for you.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="60028-275">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="60028-276">이 섹션에서는 tooWorkday 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkday.</span></span>

![사용자 할당][200] 

<span data-ttu-id="60028-278">**tooassign Britta Simon tooWorkday hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="60028-278">**tooassign Britta Simon tooWorkday, perform hello following steps:**</span></span>

1. <span data-ttu-id="60028-279">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="60028-281">Hello 응용 프로그램 목록에서 선택 **Workday**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-281">In hello applications list, select **Workday**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="60028-283">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="60028-285">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-285">Click **Add** button.</span></span> <span data-ttu-id="60028-286">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="60028-288">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60028-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="60028-289">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="60028-290">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="60028-291">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="60028-291">Testing single sign-on</span></span>

<span data-ttu-id="60028-292">Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="60028-292">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="60028-293">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="60028-293">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60028-294">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="60028-294">Additional resources</span></span>

* [<span data-ttu-id="60028-295">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="60028-295">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60028-296">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="60028-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="60028-297">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="60028-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png


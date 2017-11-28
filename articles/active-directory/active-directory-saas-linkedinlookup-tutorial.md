---
title: "자습서: LinkedIn Lookup과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory 및 LinkedIn 조회 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="7d656-103">자습서: LinkedIn Lookup과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="7d656-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="7d656-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 LinkedIn 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-104">In this tutorial, you learn how toointegrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d656-105">다음 이점을 hello로 제공 LinkedIn 조회 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="7d656-105">Integrating LinkedIn Lookup with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7d656-106">Azure ad 액세스 tooLinkedIn 조회를 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-106">You can control in Azure AD who has access tooLinkedIn Lookup</span></span>
- <span data-ttu-id="7d656-107">프로그램 사용자 tooautomatically get 로그온 tooLinkedIn 조회 (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-107">You can enable your users tooautomatically get signed-on tooLinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d656-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7d656-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d656-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7d656-110">Prerequisites</span></span>

<span data-ttu-id="7d656-111">LinkedIn 조회와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-111">tooconfigure Azure AD integration with LinkedIn Lookup, you need hello following items:</span></span>

- <span data-ttu-id="7d656-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7d656-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d656-113">LinkedIn Lookup Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7d656-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d656-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d656-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d656-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7d656-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7d656-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d656-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7d656-118">Scenario description</span></span>
<span data-ttu-id="7d656-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d656-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d656-121">LinkedIn 조회 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="7d656-121">Adding LinkedIn Lookup from hello gallery</span></span>
2. <span data-ttu-id="7d656-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7d656-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-hello-gallery"></a><span data-ttu-id="7d656-123">LinkedIn 조회 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="7d656-123">Adding LinkedIn Lookup from hello gallery</span></span>
<span data-ttu-id="7d656-124">tooconfigure hello와의 통합 LinkedIn 조회 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd LinkedIn 조회 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-124">tooconfigure hello integration of LinkedIn Lookup into Azure AD, you need tooadd LinkedIn Lookup from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7d656-125">**hello 갤러리, LinkedIn 조회 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d656-125">**tooadd LinkedIn Lookup from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d656-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7d656-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7d656-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="7d656-131">클릭 **새 응용 프로그램** hello 대화 tooadd 새 응용 프로그램의 hello 맨 위의 단추를 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="7d656-133">Hello 검색 상자에 입력 **LinkedIn 조회**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-133">In hello search box, type **LinkedIn Lookup**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="7d656-135">Hello 결과 패널에서 선택 **LinkedIn 조회**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-135">In hello results panel, select **LinkedIn Lookup**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7d656-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7d656-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7d656-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 LinkedIn Lookup에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7d656-139">Single sign on toowork에 대 한 Azure AD는 tooknow LinkedIn 조회에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Lookup is tooa user in Azure AD.</span></span> <span data-ttu-id="7d656-140">즉, Azure AD 사용자 및 LinkedIn 조회에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Lookup needs toobe established.</span></span>

<span data-ttu-id="7d656-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** LinkedIn 조회에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="7d656-142">tooconfigure 및 LinkedIn 조회를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-142">tooconfigure and test Azure AD single sign-on with LinkedIn Lookup, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7d656-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7d656-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d656-145">**[LinkedIn 조회 테스트 사용자 만들기](#creating-an-linkedin-lookup-test-user)**  -toohave Britta Simon 표현인 연결 된 Azure AD toohello LinkedIn 조회에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Lookup that is linked toohello Azure AD representation.</span></span>
4. <span data-ttu-id="7d656-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d656-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="7d656-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7d656-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7d656-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7d656-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 LinkedIn 조회 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="7d656-150">**Azure AD tooconfigure single sign on LinkedIn 조회 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d656-150">**tooconfigure Azure AD single sign-on with LinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d656-151">Hello hello에 Azure 포털에서에서 **LinkedIn 조회** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-151">In hello Azure portal, on hello **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="7d656-153">Hello에 **Single sign on** 대화에 **모드** 선택 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="7d656-155">로그온 tooyour 다른 웹 브라우저 창에서 **LinkedIn 조회** 관리자 권한으로 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-155">In a different web browser window, sign-on tooyour **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="7d656-156">**계정 센터**의 **설정** 아래에서 **전역 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="7d656-157">또한 선택 **조회** hello 드롭다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-157">Also, select **Lookup** from hello dropdown list.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="7d656-159">클릭 **또는 여기를 클릭 tooload 및 복사의에서 개별 필드 hello 양식** 복사 **엔터티 Id** 및 **Url 액세스 ACS (Assertion Consumer)**</span><span class="sxs-lookup"><span data-stu-id="7d656-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="7d656-161">Azure 포털에 아래 **LinkedIn 조회 도메인 및 Url** 섹션를 hello tooconfigure hello 응용 프로그램에 필요한 경우 다음 단계를 수행 **IDP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="7d656-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="7d656-163">a.</span><span class="sxs-lookup"><span data-stu-id="7d656-163">a.</span></span> <span data-ttu-id="7d656-164">Hello에 **식별자** textbox hello 입력 **엔터티 ID** LinkedIn 포털에서 복사</span><span class="sxs-lookup"><span data-stu-id="7d656-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="7d656-165">b.</span><span class="sxs-lookup"><span data-stu-id="7d656-165">b.</span></span> <span data-ttu-id="7d656-166">Hello에 **회신 URL** textbox hello 입력 **액세스 ACS (Assertion Consumer) Url** LinkedIn 포털에서 복사</span><span class="sxs-lookup"><span data-stu-id="7d656-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="7d656-167">확인 **고급 URL 설정 표시**tooconfigure hello 응용 프로그램에 필요한 경우, **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="7d656-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="7d656-169">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="7d656-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7d656-170">이것은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-170">This is not real value.</span></span> <span data-ttu-id="7d656-171">hello 사용자에 게 hello 사용 하 여 이러한 값 tooupdate 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-171">hello user has tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="7d656-172">연락처 [LinkedIn 조회 클라이언트 지원 팀](https://business.LinkedIn.com/lookup) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) tooget this value.</span></span>

8. <span data-ttu-id="7d656-173">프로그램 **LinkedIn 조회** 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-173">Your **LinkedIn Lookup** application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7d656-174">hello 사용자에 게 tooadd 사용자 지정 특성 매핑을 toohello SAML 토큰 특성 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-174">hello user has tooadd custom attribute mappings toohello SAML token attributes configuration.</span></span> <span data-ttu-id="7d656-175">다음 스크린 샷 hello 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-175">hello following screenshot shows an example.</span></span> <span data-ttu-id="7d656-176">기본값을 hello **사용자 식별자** 은 **user.userprincipalname** LinkedIn 조회 hello 사용자의 전자 메일 주소에 매핑이 toobe 필요 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-176">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="7d656-177">사용할 수 있습니다 **user.mail** hello 목록에서 특성 또는 사용자 조직 구성에 따라 hello 적절 한 특성 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-177">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="7d656-179">**사용자 특성** 섹션에서 클릭 **보기 및 다른 모든 사용자 특성 편집** hello 특성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-179">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="7d656-180">hello 사용자에 게 필요한 라는 tooadd 4 개의 클레임 **전자 메일**, **부서**, **firstname**, 및 **lastname** hello 값은 toobe에 매핑 **user.mail**, **user.department**, **user.givenname**, 및 **user.surname** 각각</span><span class="sxs-lookup"><span data-stu-id="7d656-180">hello user needs tooadd four claims named **email**,  **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="7d656-181">특성 이름</span><span class="sxs-lookup"><span data-stu-id="7d656-181">Attribute Name</span></span> | <span data-ttu-id="7d656-182">특성 값</span><span class="sxs-lookup"><span data-stu-id="7d656-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="7d656-183">email</span><span class="sxs-lookup"><span data-stu-id="7d656-183">email</span></span>| <span data-ttu-id="7d656-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="7d656-184">user.mail</span></span> |    
    | <span data-ttu-id="7d656-185">department</span><span class="sxs-lookup"><span data-stu-id="7d656-185">department</span></span>| <span data-ttu-id="7d656-186">user.department</span><span class="sxs-lookup"><span data-stu-id="7d656-186">user.department</span></span> |
    | <span data-ttu-id="7d656-187">firstname</span><span class="sxs-lookup"><span data-stu-id="7d656-187">firstname</span></span>| <span data-ttu-id="7d656-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7d656-188">user.givenname</span></span> |
    | <span data-ttu-id="7d656-189">lastname</span><span class="sxs-lookup"><span data-stu-id="7d656-189">lastname</span></span>| <span data-ttu-id="7d656-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="7d656-190">user.surname</span></span> |

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="7d656-192">a.</span><span class="sxs-lookup"><span data-stu-id="7d656-192">a.</span></span> <span data-ttu-id="7d656-193">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="7d656-193">Click **Add Attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="7d656-196">b.</span><span class="sxs-lookup"><span data-stu-id="7d656-196">b.</span></span> <span data-ttu-id="7d656-197">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-197">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7d656-198">c.</span><span class="sxs-lookup"><span data-stu-id="7d656-198">c.</span></span> <span data-ttu-id="7d656-199">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-199">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7d656-200">d.</span><span class="sxs-lookup"><span data-stu-id="7d656-200">d.</span></span> <span data-ttu-id="7d656-201">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-201">Click **Ok**</span></span>

10. <span data-ttu-id="7d656-202">Hello hello에서 다음 단계를 수행 **이름** 특성-</span><span class="sxs-lookup"><span data-stu-id="7d656-202">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="7d656-203">a.</span><span class="sxs-lookup"><span data-stu-id="7d656-203">a.</span></span> <span data-ttu-id="7d656-204">Hello 특성 tooopen hello 클릭 **특성 편집** 창.</span><span class="sxs-lookup"><span data-stu-id="7d656-204">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="7d656-206">b.</span><span class="sxs-lookup"><span data-stu-id="7d656-206">b.</span></span> <span data-ttu-id="7d656-207">Hello에서 hello URL 값을 삭제 **네임 스페이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-207">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="7d656-208">c.</span><span class="sxs-lookup"><span data-stu-id="7d656-208">c.</span></span> <span data-ttu-id="7d656-209">클릭 **확인** toosave hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-209">Click **Ok** toosave hello setting.</span></span>

10. <span data-ttu-id="7d656-210">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-210">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="7d656-212">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-212">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="7d656-214">너무 이동**LinkedIn 관리 설정** 섹션.</span><span class="sxs-lookup"><span data-stu-id="7d656-214">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="7d656-215">업로드 hello XML 파일 hello를 클릭 하 여 hello Azure 포털에서에서 다운로드 한 **업로드 XML 파일** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-215">Upload hello XML file you downloaded from hello Azure portal by clicking hello **Upload XML file** option.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="7d656-217">클릭 **에** tooenable SSO 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-217">Click **On** tooenable SSO.</span></span> <span data-ttu-id="7d656-218">SSO 상태에서 변경 **연결 되어 있지 않은** 너무**연결 됨**</span><span class="sxs-lookup"><span data-stu-id="7d656-218">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="7d656-220">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="7d656-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7d656-221">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="7d656-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7d656-222">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7d656-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7d656-223">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7d656-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="7d656-224">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="7d656-226">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d656-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d656-227">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-227">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7d656-229">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-229">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7d656-231">클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="7d656-231">Click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d656-233">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-233">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7d656-235">a.</span><span class="sxs-lookup"><span data-stu-id="7d656-235">a.</span></span> <span data-ttu-id="7d656-236">Hello에 **이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-236">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="7d656-237">b.</span><span class="sxs-lookup"><span data-stu-id="7d656-237">b.</span></span> <span data-ttu-id="7d656-238">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** Britta Simon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-238">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="7d656-239">c.</span><span class="sxs-lookup"><span data-stu-id="7d656-239">c.</span></span> <span data-ttu-id="7d656-240">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-240">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7d656-241">d.</span><span class="sxs-lookup"><span data-stu-id="7d656-241">d.</span></span> <span data-ttu-id="7d656-242">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="7d656-243">LinkedIn Lookup 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7d656-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="7d656-244">연결 된 조회 응용 프로그램 JIT (Time) 사용자 프로 비전 및 인증 사용자가 hello 응용 프로그램에서 자동으로 생성 한 후 마법사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="7d656-245">활성화 **자동으로 라이선스를 할당** tooassign 라이선스 toohello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-245">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7d656-247">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-247">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7d656-248">이 섹션에서는 액세스 tooLinkedIn 조회를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-248">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Lookup.</span></span>

![사용자 할당][200] 

<span data-ttu-id="7d656-250">**tooassign Britta Simon tooLinkedIn 조회를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d656-250">**tooassign Britta Simon tooLinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d656-251">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-251">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="7d656-253">Hello 응용 프로그램 목록에서 선택 **LinkedIn 조회**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-253">In hello applications list, select **LinkedIn Lookup**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="7d656-255">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-255">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="7d656-257">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-257">Click **Add** button.</span></span> <span data-ttu-id="7d656-258">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="7d656-260">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-260">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7d656-261">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d656-262">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7d656-263">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7d656-263">Testing single sign-on</span></span>

<span data-ttu-id="7d656-264">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-264">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7d656-265">Hello LinkedIn 조회 hello 액세스 패널에서에서 타일을 클릭 하면 리디렉션된 tooOrganizational 페이지 있는 tooprovide 개인 LinkedIn 계정 세부 정보 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-265">When you click hello LinkedIn Lookup tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="7d656-266">개인 계정이 LinkedIn 비즈니스 계정과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d656-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="7d656-267">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d656-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7d656-268">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7d656-268">Additional resources</span></span>

* [<span data-ttu-id="7d656-269">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="7d656-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d656-270">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7d656-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png


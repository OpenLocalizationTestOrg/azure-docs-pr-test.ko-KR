---
title: "자습서: Sprinklr와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Sprinklr 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="670c9-103">자습서: Sprinklr와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="670c9-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="670c9-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Sprinklr 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-104">In this tutorial, you learn how toointegrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="670c9-105">Azure AD와 Sprinklr 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-105">Integrating Sprinklr with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="670c9-106">액세스 tooSprinklr을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-106">You can control in Azure AD who has access tooSprinklr</span></span>
- <span data-ttu-id="670c9-107">프로그램 사용자 tooautomatically get 로그온 tooSprinklr (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-107">You can enable your users tooautomatically get signed-on tooSprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="670c9-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="670c9-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="670c9-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="670c9-110">Prerequisites</span></span>

<span data-ttu-id="670c9-111">Sprinklr과 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-111">tooconfigure Azure AD integration with Sprinklr, you need hello following items:</span></span>

- <span data-ttu-id="670c9-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="670c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="670c9-113">Sprinklr Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="670c9-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="670c9-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="670c9-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="670c9-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="670c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="670c9-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="670c9-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="670c9-118">Scenario description</span></span>
<span data-ttu-id="670c9-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="670c9-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="670c9-121">Sprinklr은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="670c9-121">Adding Sprinklr from hello gallery</span></span>
2. <span data-ttu-id="670c9-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="670c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-hello-gallery"></a><span data-ttu-id="670c9-123">Sprinklr은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="670c9-123">Adding Sprinklr from hello gallery</span></span>
<span data-ttu-id="670c9-124">tooconfigure hello와의 통합 Sprinklr Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd Sprinklr 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-124">tooconfigure hello integration of Sprinklr into Azure AD, you need tooadd Sprinklr from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="670c9-125">**Sprinklr hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="670c9-125">**tooadd Sprinklr from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="670c9-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="670c9-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="670c9-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="670c9-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="670c9-133">Hello 검색 상자에 입력 **Sprinklr**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-133">In hello search box, type **Sprinklr**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="670c9-135">Hello 결과 패널에서 선택 **Sprinklr**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-135">In hello results panel, select **Sprinklr**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="670c9-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="670c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="670c9-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Sprinklr에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="670c9-139">Single sign on toowork에 대 한 Azure AD는 tooknow Sprinklr에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sprinklr is tooa user in Azure AD.</span></span> <span data-ttu-id="670c9-140">즉, Azure AD 사용자와 Sprinklr에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-140">In other words, a link relationship between an Azure AD user and hello related user in Sprinklr needs toobe established.</span></span>

<span data-ttu-id="670c9-141">Hello hello 값을 할당, Sprinklr에서 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-141">In Sprinklr, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="670c9-142">tooconfigure와 Sprinklr과 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-142">tooconfigure and test Azure AD single sign-on with Sprinklr, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="670c9-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="670c9-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="670c9-145">**[Sprinklr 테스트 사용자 만들기](#creating-a-sprinklr-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Sprinklr에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - toohave a counterpart of Britta Simon in Sprinklr that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="670c9-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="670c9-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="670c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="670c9-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="670c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="670c9-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Sprinklr 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="670c9-150">**Azure AD tooconfigure single sign on와 Sprinklr을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="670c9-150">**tooconfigure Azure AD single sign-on with Sprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="670c9-151">Hello hello에 Azure 포털에서에서 **Sprinklr** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-151">In hello Azure portal, on hello **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="670c9-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="670c9-155">Hello에 **Sprinklr 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-155">On hello **Sprinklr Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="670c9-157">a.</span><span class="sxs-lookup"><span data-stu-id="670c9-157">a.</span></span> <span data-ttu-id="670c9-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="670c9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="670c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="670c9-159">b.</span></span> <span data-ttu-id="670c9-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="670c9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="670c9-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-161">These values are not real.</span></span> <span data-ttu-id="670c9-162">Hello로 hello 값을 업데이트 합니다. 실제 로그온 URL과 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-162">Update hello value with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="670c9-163">연락처 [Sprinklr 클라이언트 지원 팀](https://www.sprinklr.com/contact-us/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="670c9-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="670c9-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="670c9-168">Hello에 **Sprinklr 구성** 섹션에서 클릭 **구성 Sprinklr** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="670c9-168">On hello **Sprinklr Configuration** section, click **Configure Sprinklr** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="670c9-169">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="670c9-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

7. <span data-ttu-id="670c9-170">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Sprinklr 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-170">In a different web browser window, log in tooyour Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="670c9-171">너무 이동**관리 \> 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-171">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="670c9-172">![관리](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "관리")</span><span class="sxs-lookup"><span data-stu-id="670c9-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="670c9-173">너무 이동**관리 파트너 \> Single Sign** 에 hello 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="670c9-173">Go too**Manage Partner \> Single Sign** on from hello left pane.</span></span>
   
    <span data-ttu-id="670c9-174">![파트너 관리](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "파트너 관리")</span><span class="sxs-lookup"><span data-stu-id="670c9-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="670c9-175">**+Single Sign On 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="670c9-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span><span class="sxs-lookup"><span data-stu-id="670c9-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="670c9-177">Hello에 **Single Sign on** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-177">On hello **Single Sign on** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="670c9-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span><span class="sxs-lookup"><span data-stu-id="670c9-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="670c9-179">a.</span><span class="sxs-lookup"><span data-stu-id="670c9-179">a.</span></span> <span data-ttu-id="670c9-180">Hello에 **이름** 텍스트 상자 구성 이름 입력 합니다 (예: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="670c9-180">In hello **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="670c9-181">b.</span><span class="sxs-lookup"><span data-stu-id="670c9-181">b.</span></span> <span data-ttu-id="670c9-182">**사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-182">Select **Enabled**.</span></span>

    <span data-ttu-id="670c9-183">c.</span><span class="sxs-lookup"><span data-stu-id="670c9-183">c.</span></span> <span data-ttu-id="670c9-184">**새 SSO 인증서 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="670c9-185">e.</span><span class="sxs-lookup"><span data-stu-id="670c9-185">e.</span></span> <span data-ttu-id="670c9-186">콘텐츠를 클립보드에 복사 hello 메모장에서 e-64로 인코딩된 인증서를 열고 toohello 붙여 **Id 공급자 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-186">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="670c9-187">f.</span><span class="sxs-lookup"><span data-stu-id="670c9-187">f.</span></span> <span data-ttu-id="670c9-188">붙여넣기 hello **SAML 엔터티 ID** hello에 Azure 포털에서 복사한 값으로 **엔터티 Id** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-188">Paste hello **SAML Entity ID** value which you have copied from Azure Portal into hello **Entity Id** textbox.</span></span>

    <span data-ttu-id="670c9-189">g.</span><span class="sxs-lookup"><span data-stu-id="670c9-189">g.</span></span> <span data-ttu-id="670c9-190">붙여넣기 hello **SAML Single Sign-on 서비스 URL** hello에 Azure 포털에서 복사한 값으로 **Id 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="670c9-191">h.</span><span class="sxs-lookup"><span data-stu-id="670c9-191">h.</span></span> <span data-ttu-id="670c9-192">붙여넣기 hello **Sign-Out URL** hello에 Azure 포털에서 복사한 값으로 **Identity Provider Logout URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-192">Paste hello **Sign-Out URL** value which you have copied from Azure Portal into hello **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="670c9-193">i.</span><span class="sxs-lookup"><span data-stu-id="670c9-193">i.</span></span> <span data-ttu-id="670c9-194">**SAML 사용자 형식**에서 **어설션에 사용자의 sprinklr.com 사용자 이름 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="670c9-195">j.</span><span class="sxs-lookup"><span data-stu-id="670c9-195">j.</span></span> <span data-ttu-id="670c9-196">으로 **SAML 사용자 ID 위치**선택, **hello hello Subject 문의 Name Identifier 요소에 사용자 ID가**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-196">As **SAML User ID Location**, select **User ID is in hello Name Identifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="670c9-197">k.</span><span class="sxs-lookup"><span data-stu-id="670c9-197">k.</span></span> <span data-ttu-id="670c9-198">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-198">Click **Save**.</span></span>
       
    <span data-ttu-id="670c9-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="670c9-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="670c9-200">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="670c9-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="670c9-201">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="670c9-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="670c9-202">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="670c9-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="670c9-203">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="670c9-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="670c9-204">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="670c9-206">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="670c9-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="670c9-207">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="670c9-209">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="670c9-211">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="670c9-213">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="670c9-215">a.</span><span class="sxs-lookup"><span data-stu-id="670c9-215">a.</span></span> <span data-ttu-id="670c9-216">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="670c9-217">b.</span><span class="sxs-lookup"><span data-stu-id="670c9-217">b.</span></span> <span data-ttu-id="670c9-218">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="670c9-219">c.</span><span class="sxs-lookup"><span data-stu-id="670c9-219">c.</span></span> <span data-ttu-id="670c9-220">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="670c9-221">d.</span><span class="sxs-lookup"><span data-stu-id="670c9-221">d.</span></span> <span data-ttu-id="670c9-222">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="670c9-223">Sprinklr 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="670c9-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="670c9-224">관리자 권한으로 Sprinklr 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-224">Log in tooyour Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="670c9-225">너무 이동**관리 \> 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-225">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="670c9-226">![관리](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "관리")</span><span class="sxs-lookup"><span data-stu-id="670c9-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="670c9-227">너무 이동**관리 클라이언트 \> 사용자** hello 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="670c9-227">Go too**Manage Client \> Users** from hello left pane.</span></span>
   
    <span data-ttu-id="670c9-228">![설정](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "설정")</span><span class="sxs-lookup"><span data-stu-id="670c9-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="670c9-229">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="670c9-230">![설정](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "설정")</span><span class="sxs-lookup"><span data-stu-id="670c9-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="670c9-231">Hello에 **사용자 편집** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-231">On hello **Edit user** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="670c9-232">![사용자 편집](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "사용자 편집")</span><span class="sxs-lookup"><span data-stu-id="670c9-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="670c9-233">a.</span><span class="sxs-lookup"><span data-stu-id="670c9-233">a.</span></span> <span data-ttu-id="670c9-234">Hello에 **전자 메일**, **이름** 및 **성** tooprovision를 원하는 Azure AD 사용자 계정의 유형 hello 정보 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-234">In hello **Email**, **First Name** and **Last Name** textboxes, type hello information of an Azure AD user account you want tooprovision.</span></span>

    <span data-ttu-id="670c9-235">b.</span><span class="sxs-lookup"><span data-stu-id="670c9-235">b.</span></span> <span data-ttu-id="670c9-236">**암호 사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="670c9-237">c.</span><span class="sxs-lookup"><span data-stu-id="670c9-237">c.</span></span> <span data-ttu-id="670c9-238">**언어**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-238">Select **Language**.</span></span>

    <span data-ttu-id="670c9-239">d.</span><span class="sxs-lookup"><span data-stu-id="670c9-239">d.</span></span> <span data-ttu-id="670c9-240">**사용자 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-240">Select **User Type**.</span></span>

    <span data-ttu-id="670c9-241">e.</span><span class="sxs-lookup"><span data-stu-id="670c9-241">e.</span></span> <span data-ttu-id="670c9-242">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="670c9-243">**암호 사용 안 함** 선택한 tooenable을 통해 Id 공급자의 사용자 toolog 이상 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-243">**Password Disabled** must be selected tooenable a user toolog in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="670c9-244">너무 이동**역할**, 다음 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-244">Go too**Role**, and then perform hello following steps:</span></span>
   
    <span data-ttu-id="670c9-245">![파트너 역할](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "파트너 역할")</span><span class="sxs-lookup"><span data-stu-id="670c9-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="670c9-246">a.</span><span class="sxs-lookup"><span data-stu-id="670c9-246">a.</span></span> <span data-ttu-id="670c9-247">Hello에서 **Global** 목록에서 **모든\_권한을**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-247">From hello **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="670c9-248">b.</span><span class="sxs-lookup"><span data-stu-id="670c9-248">b.</span></span> <span data-ttu-id="670c9-249">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="670c9-250">다른 Sprinklr 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 tooprovision Sprinklr에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="670c9-251">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="670c9-252">이 섹션에서는 tooSprinklr 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSprinklr.</span></span>

![사용자 할당][200] 

<span data-ttu-id="670c9-254">**tooassign Britta Simon tooSprinklr hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="670c9-254">**tooassign Britta Simon tooSprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="670c9-255">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="670c9-257">Hello 응용 프로그램 목록에서 선택 **Sprinklr**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-257">In hello applications list, select **Sprinklr**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="670c9-259">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="670c9-261">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-261">Click **Add** button.</span></span> <span data-ttu-id="670c9-262">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="670c9-264">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="670c9-265">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="670c9-266">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="670c9-267">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="670c9-267">Testing single sign-on</span></span>

<span data-ttu-id="670c9-268">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="670c9-269">Hello 액세스 패널에 대 한 자세한 내용은 Sprinklr 응용 프로그램을 자동으로 로그온 tooyour, 참조 해야 hello 액세스 패널에서에서 hello Sprinklr 타일을 클릭할 때 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="670c9-269">When you click hello Sprinklr tile in hello Access Panel, you should get automatically signed-on tooyour Sprinklr application For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="670c9-270">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="670c9-270">Additional resources</span></span>

* [<span data-ttu-id="670c9-271">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="670c9-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="670c9-272">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="670c9-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

